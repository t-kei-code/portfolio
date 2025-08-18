<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: '採用特設サイト 株式会社TETOTE コーポレートサイト',
  url: 'https://im-t-kei.peewee.jp/tetote/',
  image: 'tetote.png',
  tasks: 'コーディング/WordPress化',
  tech: 'HTML, CSS(SCSS), JavaScript, PHP',
  duration: '1週間',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      12ページ構成の架空の採用特設サイトのコーディングを担当しました。<br>
    </template>
    <template #point>
      <h5 class="point__title">WordPressテーマ化</h5>
      <p>スタッフ紹介、ブログ投稿記事はWordPress投稿を反映させるようコーディングしました。</p>

      <h5 class="point__title">開発プロセスの効率化</h5>
      <p>・全体のSCSS設計はBEMに従い、可読性、修正のしやすさを意識しました。</p>
      <p>・コンポーネント単位のファイル管理で、修正・更新の効率化を行ないました。</p>
      <p>結果短い期間でコーディングを終えることができました。</p>
   
      <h5 class="point__title">効率的なレスポンシブ対応</h5>
      <p>レスポンシブ時にサイズ変化のある部分は、できる限りcssのclamp関数を使用し、レスポンシブ記述を減らしました。</p>

      <h5 class="point__title">Swiperスライダー</h5>
      <p>トップページのギャラリースライダーはSlickを利用。<br>
        画面幅に沿って画像表示数を制御しています。
      </p>

      <h5 class="point__title">ピクセルパーフェクト</h5>
      <p>PerfectPixelを使用し、デザインカンプに忠実なコーディングを行いました。
      </p>
    </template>

    <template #afterUrl>
    <p class="afterURL">
      ユーザー名: demo<br>
      パスワード: demo-01
    </p>
  </template>
  </WorkDetailLayout>
</template>

<style lang="scss">
  @use "@/styles/mixin" as *;
  .point__title {
    font-weight: bold;
    margin-top: 20px;
  }
</style>