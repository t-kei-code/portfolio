<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'イタリアンレストランSHU - LP',
  url: 'https://cottleya.jobtra-itweb.com/italian/',
  image: 'food.png',
  tasks: 'デザイン/コーディング',
  tech: 'Figma, Illustrator, HTML/CSS, jQuery',
  duration: '1か月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      イタリアンダイニングSHU(架空)のホームページのデザインとコーディングを行いました。
    </template>
    <template #point>
      <p>
        <h5 class="point__title">デザインコンセプト</h5>
        オフィス街にある隠れ家的イタリアン。落ち着いていておしゃれ、気軽に入店しやすい雰囲気を目指しました。
        
      </p>
      <h5 class="point__title">コーディング</h5>
      <p>全体のSCSS設計はBEMに従い、保守性を意識しました。</p>
    </template>
  </WorkDetailLayout>
</template>

<style scoped>
.img__container {
  max-width: 1200px;
  display: flex;
  justify-content: center;
  gap: 30px;
}
.img--sp {
  width: 20%;
}
.img--pc {
  width: 50%;
}
</style>
