<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import * as THREE from "three"

const canvasRef = ref(null);
onMounted(()=> {
  const camera = new THREE.PerspectiveCamera(75,window.innerWidth / window.innerHeight, 1, 1000);
  camera.position.z = 5;

  const renderer = new THREE.WebGLRenderer({
    canvas: canvasRef.value,
    alpha: true,
  })
  renderer.setSize(window.innerWidth, window.innerHeight);

  const scene = new THREE.Scene();

  const geometry = new THREE.SphereGeometry(1,128,128)
  const material = new THREE.ShaderMaterial({
  transparent: true,
  uniforms: {
    time: { value: 0 },
  },
  vertexShader: `
    uniform float time;
    varying vec3 vNormal;
    varying vec3 vWorldPosition;

    void main() {
      float frequency = 4.0;
      float amplitude = 0.1;

      //波を生成
      float offset = sin(position.y * frequency + time) * amplitude;

      //法線方向にオフセット
      vec3 newPosition = position + normal * offset;

      vNormal = normalize(normalMatrix * normal);
      vec4 worldPos = modelMatrix * vec4(newPosition, 1.0);
      vWorldPosition = worldPos.xyz;
      gl_Position = projectionMatrix * viewMatrix * worldPos;
    }

  `,
  fragmentShader: `
    varying vec3 vNormal;
    varying vec3 vWorldPosition;

    void main() {
      vec3 viewDir = normalize(cameraPosition - vWorldPosition);
      float fresnel = pow(1.0 - dot(viewDir, normalize(vNormal)), 2.0);
      vec3 color = vec3(1.0, 1.0, 1.0) * fresnel;
      gl_FragColor = vec4(color, fresnel);
    }
  `
});


  const mesh = new THREE.Mesh(geometry, material);
  mesh.position.set(1.0, 1.5, 1.0)
  scene.add(mesh);

  function onResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
  }
  window.addEventListener("resize", onResize);

  function animate() {
      requestAnimationFrame(animate)
      material.uniforms.time.value += 0.03;
      renderer.render(scene, camera)
    }
    animate();
})

</script>

<template>
  <canvas ref="canvasRef"></canvas>
</template>

<style scoped lang="scss">
  canvas {
    position: absolute;
    top: 0;
    left: 0;
  }

</style>
