<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'SPORTHERE -LP',
  url: 'https://cottleya.jobtra-itweb.com/SPORTHERE/',
  image: 'sport.png',
  tasks: 'コーディング/',
  tech: 'html, css',
  duration: '1週間',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData" />
</template>
