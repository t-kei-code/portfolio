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
      <p>
        女性らしい柔らかさと、みずみずしく上品な印象を目指しました。
        白や淡いブルーを基調に柔らかさと透明感を表現しました。
        テキストは明朝体で上品さを演出しています。
      </p>
    </template>
  </WorkDetailLayout>
</template>
