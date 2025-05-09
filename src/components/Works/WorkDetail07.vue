<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'レンタルカメラサービス バナー',
  image: 'camera.png',
  tasks: 'デザイン/',
  tech: 'illustrator, photoshop',
  duration: '20日',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData" />
</template>
