<script setup>
import * as THREE from "three"
import { ref, onMounted } from "vue"
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls"

const canvasRef = ref(null)

onMounted(() => {
  const scene = new THREE.Scene()
  const renderer = new THREE.WebGLRenderer({
    canvas: canvasRef.value,
    antialias: true,
    alpha: true,
  })
  const height = 400
  renderer.setSize(window.innerWidth, height)

  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / height,
    0.1,
    1000
  )
  camera.position.set(0, 0, 6)

  const controls = new OrbitControls(camera, renderer.domElement)
  controls.enableDamping = true

  // ====== カードパラメータ ======
  const count = 7 // カード枚数
  const ringRadius = 2.4 // リングの半径
  const cardWidth = 1.5   // カード横幅
  const cardHeight = 1.1  // カード縦幅
  const cardCurveR = 3.5  // カード1枚の“カーブの半径”（大きいとゆるい）

  for (let i = 0; i < count; i++) {
    // カーブしたPlaneジオメトリを生成
    const segments = 30
    const geometry = new THREE.PlaneGeometry(cardWidth, cardHeight, segments, 1)

    // カーブ加工：x方向の頂点を円弧状に変形
    const pos = geometry.attributes.position
    for (let s = 0; s <= segments; s++) {
      const x = (s / segments - 0.5) * cardWidth
      const theta = x / cardCurveR
      for (let t = 0; t <= 1; t++) {
        const idx = s * 2 + t
        pos.setX(idx, Math.sin(theta) * cardCurveR)
        pos.setZ(idx, cardCurveR - Math.cos(theta) * cardCurveR)
      }
    }
    pos.needsUpdate = true

    // マテリアル（色はHSLでカラフルに）
    const material = new THREE.MeshBasicMaterial({
      color: new THREE.Color(`hsl(${(i / count) * 360}, 70%, 60%)`),
      side: THREE.DoubleSide,
      transparent: true,
      opacity: 0.92,
    })
    const card = new THREE.Mesh(geometry, material)

    // リング上の配置
    const angle = (i / count) * Math.PI * 2
    card.position.x = Math.cos(angle) * ringRadius
    card.position.z = Math.sin(angle) * ringRadius

    // 原点を向けることでリングに“張り付く”＋カーブ方向も自然になる
    card.lookAt(0, 0, 0)

    scene.add(card)
  }

  // ==== アニメーション ====
  function animate() {
    requestAnimationFrame(animate)
    controls.update()
    renderer.render(scene, camera)
  }
  animate()
})
</script>

<template>
  <h3>Three.js作品（リング＆カーブデモ）</h3>
  <canvas ref="canvasRef"></canvas>
</template>
