<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { perlin } from '../../perlin.js'

const canvasRef = ref(null)
let ctx
let animationFrameId // アニメーションをキャンセルするためのID
let time = 0

function drawWave() {
  if (!ctx) return

  ctx.clearRect(0, 0, canvasRef.value.width, canvasRef.value.height)
  ctx.strokeStyle = 'rgba(181, 190, 207, 0.5)'
  ctx.lineWidth = 2

  const numWaves = 10
  const waveSpeed = 0.01
  const noiseScale = 0.005

  for (let i = 0; i < numWaves; i++) {
    ctx.beginPath()
    for (let x = 0; x < canvasRef.value.width; x += 10) {
      let noiseVal = perlin.get(x * noiseScale, time * noiseScale) * 50
      let y = canvasRef.value.height / 2 + Math.sin(x * 0.01 + time - i * 0.3) * 100 + noiseVal
      ctx.lineTo(x, y)
    }
    ctx.stroke()
  }

  time += waveSpeed
  animationFrameId = requestAnimationFrame(drawWave)
}

function handleResize() {
  if (!canvasRef.value) return
  canvasRef.value.width = window.innerWidth
  canvasRef.value.height = window.innerHeight
}

onMounted(() => {
  const canvas = canvasRef.value
  if (!canvas) return

  ctx = canvas.getContext('2d')

  handleResize()

  // キャンバスのサイズを設定
  canvas.width = window.innerWidth
  canvas.height = window.innerHeight

  drawWave() // アニメーション開始
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  if (animationFrameId) cancelAnimationFrame(animationFrameId)
  window.removeEventListener('resize', handleResize)
  ctx = null // ctx を解放
})

</script>

<template>
  <canvas class="waveCanvas" ref="canvasRef"></canvas>
</template>

<style scoped>
canvas {
  position: absolute;
  inset: 0;
  opacity: 0.5;
}
</style>
