<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import * as THREE from 'three'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
import gsap from 'gsap'
import router from '@/router'

const canvasRef = ref(null)

let modelA, positionA, modelB, positionB, modelC, positionC
let material, geometry, particles
let group, scene, renderer, camera, light, loader3d, animationId
let gsapTimeline
let isMounted = true
const clock = new THREE.Clock()
const opacity = ref(1)

function isMobileDevice() {
  return /iPhone|iPad|iPod|Android/i.test(navigator.userAgent)
}

function samplePositions(positions, interval = 2) {
  const sampled = []
  for (let i = 0; i < positions.length; i += 3 * interval) {
    sampled.push(positions[i], positions[i + 1], positions[i + 2])
  }
  return sampled
}

function extractPosition(model, scale = 1) {
  model.updateMatrixWorld(true)
  let positions = []

  model.traverse((child) => {
    if (child instanceof THREE.Mesh) {
      const posAttr = child.geometry.attributes.position
      const tempVec = new THREE.Vector3()

      for (let i = 0; i < posAttr.count; i++) {
        tempVec.set(
          posAttr.getX(i) * scale,
          posAttr.getY(i) * scale,
          posAttr.getZ(i) * scale
        )
        tempVec.applyMatrix4(child.matrixWorld)
        positions.push(tempVec.x, tempVec.y, tempVec.z)
      }
    }
  })

  return isMobileDevice() ? samplePositions(positions, 2) : positions
}

function onResize() {
  if (!camera || !renderer || !canvasRef.value) return
  const width = window.innerWidth
  const height = window.innerHeight
  const dpr = Math.min(window.devicePixelRatio || 1, 2)

  camera.aspect = width / height
  camera.updateProjectionMatrix()

  renderer.setSize(width, height)
  renderer.setPixelRatio(dpr)

  let groupScale = width < 768 ? 0.8 : width < 1024 ? 1.0 : 1.6
  group.scale.set(groupScale, groupScale, groupScale)

  if (modelA && modelB && modelC && geometry) {
    positionA = extractPosition(modelA)
    positionB = extractPosition(modelB)
    positionC = extractPosition(modelC)

    geometry.setAttribute('position', new THREE.Float32BufferAttribute(positionA, 3))
    geometry.setAttribute('modelAPosition', new THREE.Float32BufferAttribute(positionA, 3))
    geometry.setAttribute('modelBPosition', new THREE.Float32BufferAttribute(positionB, 3))
    geometry.setAttribute('modelCPosition', new THREE.Float32BufferAttribute(positionC, 3))
  }
}

function checkAndCreateParticles() {
  if (positionA && positionB && positionC) createParticle()
}

function createParticle() {
  geometry = new THREE.BufferGeometry()
  geometry.setAttribute('position', new THREE.Float32BufferAttribute(positionA, 3))
  geometry.setAttribute('modelAPosition', new THREE.Float32BufferAttribute(positionA, 3))
  geometry.setAttribute('modelBPosition', new THREE.Float32BufferAttribute(positionB, 3))
  geometry.setAttribute('modelCPosition', new THREE.Float32BufferAttribute(positionC, 3))

  material = new THREE.ShaderMaterial({
    uniforms: {
      uMorph: { value: 0.0 },
      uColor: { value: new THREE.Color('darkgray') },
      opacity: { value: opacity.value },
    },
    vertexShader: `
      uniform float uMorph;
      attribute vec3 modelAPosition;
      attribute vec3 modelBPosition;
      attribute vec3 modelCPosition;
      vec3 morphed;

      void main() {
        if (uMorph < 1.0) {
          morphed = mix(modelAPosition, modelBPosition, uMorph);
        } else if (uMorph < 2.0) {
          morphed = mix(modelBPosition, modelCPosition, uMorph - 1.0);
        } else {
          morphed = mix(modelCPosition, modelAPosition, uMorph - 2.0);
        }
        gl_Position = projectionMatrix * modelViewMatrix * vec4(morphed, 1.0);
        gl_PointSize = 2.0;
      }
    `,
    fragmentShader: `
      uniform vec3 uColor;
      uniform float opacity;
      void main() {
        gl_FragColor = vec4(uColor, opacity);
      }
    `,
    transparent: true,
    depthWrite: false,
    blending: THREE.AdditiveBlending,
  })

  particles = new THREE.Points(geometry, material)
  group.add(particles)
  group.position.set(2, -0.7, 0)
  morphingAnimation()
}

function morphingAnimation() {
  gsapTimeline = gsap.timeline({ repeat: -1 })
    .to(material.uniforms.uMorph, { value: 1, duration: 2 })
    .to(material.uniforms.uMorph, { value: 1, duration: 0, delay: 5 })
    .to(material.uniforms.uMorph, { value: 2, duration: 2 })
    .to(material.uniforms.uMorph, { value: 2, duration: 0, delay: 5 })
    .to(material.uniforms.uMorph, { value: 3, duration: 2 })
    .to(material.uniforms.uMorph, { value: 3, duration: 0, delay: 5 })
    .to(material.uniforms.uMorph, { value: 0, duration: 0 })
}

function animate() {
  if (!isMounted) return
  animationId = requestAnimationFrame(animate)
  const elapsedTime = clock.getElapsedTime()
  group.rotation.y = elapsedTime * 0.5
  material?.uniforms.opacity && (material.uniforms.opacity.value = opacity.value)
  renderer.render(scene, camera)
}

onMounted(() => {
  if (!canvasRef.value) return

  scene = new THREE.Scene()
  renderer = new THREE.WebGLRenderer({ canvas: canvasRef.value, antialias: true, alpha: true })
  renderer.setSize(window.innerWidth, window.innerHeight)
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 5

  light = new THREE.DirectionalLight(0xffffff, 2)
  light.position.set(5, 10, 5)
  scene.add(light)

  group = new THREE.Group()
  scene.add(group)

  loader3d = new GLTFLoader()
  loader3d.load('hourglass8.glb', (g) => { modelA = g.scene; positionA = extractPosition(modelA); checkAndCreateParticles() })
  loader3d.load('gear.glb', (g) => { modelB = g.scene; positionB = extractPosition(modelB); checkAndCreateParticles() })
  loader3d.load('box7.glb', (g) => { modelC = g.scene; positionC = extractPosition(modelC); checkAndCreateParticles() })

  window.addEventListener('resize', onResize)
  animate()
})

function gotoAbout() {
  gsap.to(opacity, {
    value: 0,
    duration: 0.3,
    onComplete: () => router.push("/about")
  })
}

onUnmounted(() => {
  isMounted = false
  cancelAnimationFrame(animationId)
  gsapTimeline?.kill()
  window.removeEventListener('resize', onResize)
})
</script>

<template>
  <canvas class="mainCanvas" ref="canvasRef"></canvas>
</template>

<style scoped>
.mainCanvas {
  position: absolute;
  top: 0;
  left: 0;
  inset: 0;
  width: 100vw;
  height: 100vh;
  display: block;
}
</style>
