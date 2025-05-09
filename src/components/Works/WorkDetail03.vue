<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '',
  title: '',
  url: '',
  image: '',
  tasks: '',
  tech: '',
  duration: '',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData" />
</template>
