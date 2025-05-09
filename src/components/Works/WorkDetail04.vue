<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'たいよう保育園 LP',
  url: 'https://cottleya.jobtra-itweb.com/taiyo-preschool/',
  image: 'taiyo.png',
  tasks: 'デザイン/コーディング/',
  tech: 'html, css',
  duration: '1ヶ月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData" />
</template>
