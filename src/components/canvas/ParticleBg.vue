<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import * as THREE from 'three'

const canvasRef = ref(null)
let renderer, scene, camera, particles, speeds, animationId
let material, geometry
const clock = new THREE.Clock() // ⏳ FPS に依存しないための Clock

function onResize() {
  if (!camera || !renderer || !canvasRef.value) return

  const width = window.innerWidth
  const height = window.innerHeight
  const dpr = window.devicePixelRatio || 1

  camera.aspect = width / height
  camera.updateProjectionMatrix()

  renderer.setSize(width, height)
  renderer.setPixelRatio(dpr)
}

onMounted(() => {
  if (!canvasRef.value) return

  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 5

  renderer = new THREE.WebGLRenderer({
    canvas: canvasRef.value,
    alpha: true,
  })
  renderer.setSize(window.innerWidth, window.innerHeight)

  const particleTexture = new THREE.TextureLoader().load('circle.png')

  geometry = new THREE.BufferGeometry()
  const count = 700
  const positions = new Float32Array(count * 3)
  speeds = new Float32Array(count * 3)

  for (let i = 0; i < count; i++) {
    positions[i * 3] = (Math.random() - 0.5) * 100
    positions[i * 3 + 1] = (Math.random() - 0.5) * 70
    positions[i * 3 + 2] = Math.random() * -30 - 10

    speeds[i * 3] = (Math.random() - 0.5) * 0.02
    speeds[i * 3 + 1] = (Math.random() - 0.5) * 0.02
  }

  geometry.setAttribute('position', new THREE.Float32BufferAttribute(positions, 3))

  material = new THREE.PointsMaterial({
    map: particleTexture,
    color: 'white',
    size: 0.2,
    transparent: true,
    opacity: 0.8,
    depthWrite: false,
    blending: THREE.AdditiveBlending,
  })

  particles = new THREE.Points(geometry, material)
  scene.add(particles)

  function animate() {
    animationId = requestAnimationFrame(animate)

    const elapsedTime = clock.getElapsedTime() // ⏳ 経過時間（秒）

    const positionsArray = particles.geometry.attributes.position.array
    for (let i = 0; i < count; i++) {
      positionsArray[i * 3] += Math.sin(elapsedTime * 0.2 + i) * speeds[i * 3] // ⏳ 経過時間を使う
      positionsArray[i * 3 + 1] += Math.sin(elapsedTime * 0.3 + i) * speeds[i * 3 + 1]
    }

    particles.geometry.attributes.position.needsUpdate = true
    renderer.render(scene, camera)
  }

  animate()
  window.addEventListener('resize', onResize)
})

onUnmounted(() => {
  window.removeEventListener('resize', onResize)
  cancelAnimationFrame(animationId)

  if (renderer) {
    renderer.dispose()
    renderer = null
  }

  if (material) {
    material.dispose()
    material = null
  }

  if (geometry) {
    geometry.dispose()
    geometry = null
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
  <canvas class="bgCanvas" ref="canvasRef"></canvas>
</template>

<style scoped>
canvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: linear-gradient(
    90deg,
    rgba(131, 131, 131, 1),
    rgba(92, 90, 90, 1) 53%,
    rgba(60, 54, 54, 1)
  );
  background: linear-gradient(to bottom, hsl(180, 4%, 40%), hsl(240, 12%, 51%), hsl(226, 60%, 7%));
  background-size: 400% 400%;
  animation: AnimationName 10s ease infinite;
}

@keyframes AnimationName {
  0% {
    background-position: 50% 0%;
  }
  50% {
    background-position: 50% 100%;
  }
  100% {
    background-position: 50% 0%;
  }
}
</style>
