<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'SPORTHERE -LP',
  url: 'https://cottleya.jobtra-itweb.com/SPORTHERE/',
  image: 'sport.png',
  tasks: 'コーディング/',
  tech: 'HTML, CSS',
  duration: '1週間',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      スポーツ事業会社の自社アプリ「SPORTHERE」の紹介LPサイトコーディングを行いました。
    </template>
    <template #point>
      全体のSCSS設計はBEMに従い、保守性を意識しました。
    </template>
  </WorkDetailLayout>
</template>
