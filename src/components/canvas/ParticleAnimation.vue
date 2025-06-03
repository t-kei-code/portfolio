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
let gsapTimeline, resizeTimeout
let isMounted = true
const clock = new THREE.Clock()
const opacity = ref(1)
const isMobile = window.innerWidth < 768

function extractPosition(model, scale = 1) {
  model.updateMatrixWorld(true)
  let positions = []
  model.traverse((child) => {
    if (child instanceof THREE.Mesh) {
      const attr = child.geometry.attributes.position
      const tempVec = new THREE.Vector3()
      for (let i = 0; i < attr.count; i++) {
        tempVec.set(attr.getX(i) * scale, attr.getY(i) * scale, attr.getZ(i) * scale)
        tempVec.applyMatrix4(child.matrixWorld)
        positions.push(tempVec.x, tempVec.y, tempVec.z)
      }
    }
  })
  return positions
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
  if (group) {
    let groupScale = width < 768 ? 0.8 : width < 1440 ? 1 : 1.4
    group.scale.set(groupScale, groupScale, groupScale)
  }
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

function debounceResize() {
  clearTimeout(resizeTimeout)
  resizeTimeout = setTimeout(() => {
    onResize()
    renderer.render(scene, camera)
  }, 200)
}

function createParticle() {
  if (!positionA || !positionB || !positionC) return
  geometry = new THREE.BufferGeometry()
  geometry.setAttribute('position', new THREE.Float32BufferAttribute(positionA, 3))
  geometry.setAttribute('modelAPosition', new THREE.Float32BufferAttribute(positionA, 3))
  geometry.setAttribute('modelBPosition', new THREE.Float32BufferAttribute(positionB, 3))
  geometry.setAttribute('modelCPosition', new THREE.Float32BufferAttribute(positionC, 3))
  material = new THREE.ShaderMaterial({
    uniforms: {
      uMorph: { value: 0.0 },
      uColor: { value: new THREE.Color('darkgray') },
      opacity: { value: opacity.value }
    },
    vertexShader: `
      uniform float uMorph;
      attribute vec3 modelAPosition;
      attribute vec3 modelBPosition;
      attribute vec3 modelCPosition;
      void main() {
        vec3 morphed = uMorph < 1.0 ? mix(modelAPosition, modelBPosition, uMorph) :
                        uMorph < 2.0 ? mix(modelBPosition, modelCPosition, uMorph - 1.0) :
                                       mix(modelCPosition, modelAPosition, uMorph - 2.0);
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
    blending: THREE.AdditiveBlending
  })
  particles = new THREE.Points(geometry, material)
  group.add(particles)
  group.position.set(2, -0.7, 0)
  morphingAnimation()
}

function morphingAnimation() {
  if (!material || !material.uniforms.uMorph) return
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
  if (group) group.rotation.y = elapsedTime * 0.5
  if (material?.uniforms.opacity) material.uniforms.opacity.value = opacity.value
  renderer.render(scene, camera)
}

onMounted(() => {
  if (!canvasRef.value) return
  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 5
  renderer = new THREE.WebGLRenderer({ canvas: canvasRef.value, alpha: true, antialias: true })
  renderer.setSize(window.innerWidth, window.innerHeight)
  group = new THREE.Group()
  scene.add(group)
  light = new THREE.DirectionalLight(0xffffff, 2)
  light.position.set(5, 10, 5)
  scene.add(light)
  loader3d = new GLTFLoader()

  if (isMobile) {
    loader3d.load('gear3.glb', (glb) => {
      modelA = glb.scene
      positionA = extractPosition(modelA)
      positionB = positionC = positionA
      createParticle()
    })
  } else {
    loader3d.load('gear3.glb', (glb) => {
      modelA = glb.scene
      positionA = extractPosition(modelA)
      check()
    })
    loader3d.load('hourglass05.glb', (glb) => {
      modelB = glb.scene
      positionB = extractPosition(modelB)
      check()
    })
    loader3d.load('box04.glb', (glb) => {
      modelC = glb.scene
      positionC = extractPosition(modelC)
      check()
    })
  }

  function check() {
    if (positionA && positionB && positionC) createParticle()
  }

  window.addEventListener('resize', debounceResize)
  animate()
  requestAnimationFrame(() => onResize())
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
  window.removeEventListener('resize', debounceResize)
})
</script>

<template>
  <canvas class="mainCanvas" ref="canvasRef"></canvas>
</template>

<style scoped>
.mainCanvas {
  position: absolute;
  inset: 0;
  width: 100vw;
  height: 100vh;
  display: block;
  touch-action: none;
}
</style>
