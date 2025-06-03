<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '個人製作',
  title: 'KEI TSUKAMOTO - ポートフォリオサイト',
  url: 'im-t-kei-portfolio.netlify.app',
  image: 'portfolio.png',
  tasks: 'デザイン/コーディング/',
  tech: 'html, css(scss), javascript, vue.js, Three.js, gsap, blender',
  duration: '3ヶ月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      本ポートフォリオサイト
    </template>
    <template #point>
      本ポートフォリオサイトです。自身の持っている技術スタックを総動員して制作しました。
      メインビジュアルではblenderで制作したオブジェクトをthree.jsでパーティ化し、
      gsapでアニメーション制御を行っています。またメインシステムはvue.jsで構築し、
      シームレスなページ遷移と効率的なコード設計を実現しました。
      <!-- <img src="/public/スクリーンショット 2025-05-23 121106.png" alt="" srcset=""> -->
    </template>
  </WorkDetailLayout>
</template>
