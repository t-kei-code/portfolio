<script setup>
import * as THREE from 'three'
import { onMounted, onUnmounted, ref } from 'vue'

const canvasRef = ref(null)
let scene, camera, renderer, point, particleMaterial
let animationFrameId

function onResize() {
  if (!renderer || !camera) return
  renderer.setSize(window.innerWidth, window.innerHeight)
  camera.aspect = window.innerWidth / window.innerHeight
  camera.updateProjectionMatrix()
}

onMounted(() => {
  if (!canvasRef.value) return

  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(50, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 5

  renderer = new THREE.WebGLRenderer({
    canvas: canvasRef.value,
    alpha: true,
  })
  renderer.setSize(window.innerWidth, window.innerHeight)
  renderer.setPixelRatio(window.devicePixelRatio)

  const canvas01 = document.createElement('canvas')
  let uTime = { value: 0.0 }
  const baseURL = import.meta.env.BASE_URL
  const images = [baseURL + 'headerTtlAbout.png']
  let particles1 = [],
    colors1 = []

  function loadImage(imageSrc, callback) {
    const img = new Image()
    img.crossOrigin = 'Anonymous'
    img.src = imageSrc
    img.onload = () => {
      const ctx = canvas01.getContext('2d')
      canvas01.width = img.width
      canvas01.height = img.height
      ctx.drawImage(img, 0, 0)
      const data = ctx.getImageData(0, 0, img.width, img.height).data

      const particles = []
      const colors = []
      const space = 4

      for (let y = 0; y < img.height; y += space) {
        for (let x = 0; x < img.width; x += space) {
          const index = (y * img.width + x) * 4
          const r = data[index] / 255
          const g = data[index + 1] / 255
          const b = data[index + 2] / 255
          const a = data[index + 3]

          if (a > 100) {
            const posX = (x - img.width / 2) * 0.015
            const posY = (y - img.height / 2) * -0.015
            particles.push(posX, posY, 0)
            colors.push(r, g, b)
          }
        }
      }
      callback(particles, colors)
    }
  }

  loadImage(images[0], (p, c) => {
    particles1 = p
    colors1 = c
    createParticles()
  })

  function createParticles() {
    if (particles1.length === 0) return

    const randomOffsets = []
    for (let i = 0; i < particles1.length; i += 3) {
      randomOffsets.push(
        (Math.random() - 0.5) * 2.0,
        (Math.random() - 0.5) * 2.0,
        (Math.random() - 0.5) * 2.0,
      )
    }

    const particleGeometry = new THREE.BufferGeometry()
    particleGeometry.setAttribute('position', new THREE.Float32BufferAttribute(particles1, 3))
    particleGeometry.setAttribute('randomPos', new THREE.Float32BufferAttribute(randomOffsets, 3))
    particleGeometry.setAttribute('color', new THREE.Float32BufferAttribute(colors1, 3))

    particleMaterial = new THREE.ShaderMaterial({
      uniforms: { uTime: uTime },
      vertexShader: `
      attribute vec3 randomPos;
      varying vec3 vColor;
      uniform float uTime;

      void main() {
        float t = smoothstep(0.0, 0.5, uTime);
        vec3 tempPos = mix(position + randomPos * sin(uTime * 10.0), position, t);
        vColor = mix(vec3(1.0, 1.0, 1.0), vec3(0.0, 1.0, 1.0), uTime);
        gl_Position = projectionMatrix * modelViewMatrix * vec4(tempPos, 1.0);
        gl_PointSize = 8.0 + sin(uTime * 20.0) * 4.0;
      }
    `,
      fragmentShader: `
      varying vec3 vColor;
      void main() {
        float r = length(gl_PointCoord - vec2(0.5));
        if (r > 0.5) discard;
        gl_FragColor = vec4(vColor, 1.0);
      }
    `,
      transparent: true,
    })

    point = new THREE.Points(particleGeometry, particleMaterial)
    scene.add(point)
  }

  function animate() {
    if (!renderer || !scene || !camera) return
    animationFrameId = requestAnimationFrame(animate)
    renderer.render(scene, camera)
  }

  animate()
  window.addEventListener('resize', onResize)
})

onUnmounted(() => {
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId)
    animationFrameId = null
  }

  window.removeEventListener('resize', onResize)

  if (point) {
    scene.remove(point)
    point.geometry.dispose()
    if (point.material) point.material.dispose()
  }

  if (renderer) {
    renderer.dispose()
    renderer = null
  }

  if (scene) {
    scene.clear()
    scene = null
  }

  if (camera) {
    camera = null
  }
})
</script>

<template>
  <canvas class="textCanvas" ref="canvasRef"></canvas>
</template>

<style scoped>
canvas {
  width: 100vw;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
