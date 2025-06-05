<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'イタリアンレストランSHU - LP',
  // url: 'url',
  image: 'food.png',
  tasks: 'デザイン/',
  tech: 'Figma, Illustrator ',
  duration: '20日',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      イタリアンダイニングSHU(架空)のホームページのデザインとコーディングを行いました。
    </template>
    <template #point>
      <p>
        オフィス街にある隠れ家的イタリアン。落ち着いていておしゃれ、気軽に行ける雰囲気を目指しました。
      </p>
      <p>コアターゲット：新卒入社のOL 気軽に先輩を誘える店が欲しいと思っている。</p>
    </template>
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
