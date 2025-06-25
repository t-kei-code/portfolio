<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: '洗顔用化粧水バナー',
  image: 'kesyousui.jpg',
  tasks: 'デザイン',
  tech: 'Illustrator, Photoshop',
  duration: '2日',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      洗顔用化粧品・クレンジング HADAMIRAI(架空)の新商品告知バナーのデザインを制作しました。
    </template>
    <template #point>
      <h5 class="point__title">デザインコンセプト</h5>
      <p>みずみずしく上品な印象を目指しました。</p>
        女性らしい柔らかさと上品さ、みずみずしい感じや透明、
      <p>白や淡いブルーを使用し、柔らかさと透明感を表現しました。</p>
    </template>
  </WorkDetailLayout>
</template>
