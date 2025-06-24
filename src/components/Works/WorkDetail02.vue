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
        本ポートフォリオサイトです。<br>
        Vue.js + Three.jsで構築しました。3Dアニメーションやページ遷移演出を取り入れた動きのあるサイト表現に挑戦しました。
    </template>
    <template #point>
      

      
      <h5 class="point__title">3Dアニメーション実装</h5>
      <p>
        メインビジュアルには、Blenderで制作した3DオブジェクトをThree.jsで読み込み、パーティクル（粒子）状に変換して変形させるアニメーションを実装しています。
      </p>

      <h5 class="point__title">効率的な開発フロー</h5>
      <p>・全体のSCSS設計はBEMに従い、可読性、修正のしやすさを意識しました。</p>
      <p>・コンポーネント単位のファイル管理で、修正・更新の効率化を行ないました。</p>
      <p>・制作物のデータはVue.jsでオブジェクトとして管理し、簡単に掲載物の入れ替えを行えるようにしました。</p>

      <h5></h5>
      

      <h5 class="point__title">開発環境</h5>
      開発環境にはViteを使用し、ソースコードの管理にはGit、公開にはNetlifyを利用しています。

      
      <!-- <img src="/public/スクリーンショット 2025-05-23 121106.png" alt="" srcset=""> -->
    </template>
  </WorkDetailLayout>
</template>
