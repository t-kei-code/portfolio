<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'イタリアンレストランSHU - LP',
  // url: 'url',
  image: 'food.png',
  tasks: 'デザイン/',
  tech: 'figma, illustrator ',
  duration: '20日',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <p>イタリアンレストランSHU様(架空)のLPサイトを制作しました。</p>
  </WorkDetailLayout>
  <div class="img__container">
    <img class="img--sp" src="/spサイズ.jpg" alt="" />
    <img class="img--pc" src="/pcサイズ.jpg" alt="" />
  </div>
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
