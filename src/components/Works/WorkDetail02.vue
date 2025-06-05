<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '個人製作',
  title: 'KEI TSUKAMOTO - ポートフォリオサイト',
  url: 'im-t-kei-portfolio.netlify.app/',
  image: 'portfolio.png',
  tasks: 'デザイン/コーディング/',
  tech: 'HTML, CSS(SCSS), JavaScript, Vue.js, Three.js, gsap, Blender',
  duration: '4ヶ月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      本ポートフォリオサイト
    </template>
    <template #point>
      本ポートフォリオサイトです。<br>
      Vue.js + Three.jsで構築しました。3Dアニメーションやページ遷移演出を取り入れた動きのあるサイト表現に挑戦しました。
      <p>
        メインビジュアルではBlenderで制作した3Dオブジェクトデータをthree.jsでパーティクル(粒子)化し、変形のアニメーションを実装しました。<br>
        ※パフォーマンスの問題や、スマホ表示時の表示問題があり、現在も修正作業中です。
      </p>
      <!-- <img src="/public/スクリーンショット 2025-05-23 121106.png" alt="" srcset=""> -->
    </template>
  </WorkDetailLayout>
</template>
