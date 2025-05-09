<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '個人製作',
  title: 'KEI TSUKAMOTO - ポートフォリオサイト',
  url: 'https://im-t-kei.peewee.jp/portfolio/',
  image: 'portfolio.png',
  tasks: 'デザイン/コーディング/',
  tech: 'html, css(scss), javascript, vue.js, Three.js, gsap, blender',
  duration: '3ヶ月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <p>
      本ポートフォリオサイトです。自身の持っている技術スタックを総動員して制作しました。
      メインビジュアルではblenderで制作したオブジェクトをthree.jsでパーティ化し、
      gsapでアニメーション制御を行っています。またメインシステムはvue.jsで構築し、
      シームレスなページ遷移と効率的なコード設計を実現しました。
    </p>
    <p>鋭意制作中。</p>
  </WorkDetailLayout>
</template>
