<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: '青牡丹工務店 コーポレートサイト',
  url: 'https://im-t-kei.peewee.jp/aobotan/',
  image: 'aobotan.png',
  tasks: 'コーディング',
  tech: 'HTML, SCSS,Javascript,Jquery',
  duration: '20日',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      5ページ構成の架空の工務店コーポレートサイトのコーディングを担当しました。
    </template>
    <template #point>
     
      <h5 class="point__title">開発プロセスの効率化</h5>
      <p>・全体のSCSS設計はBEMに従い、可読性、修正のしやすさを意識しました。</p>
      <p>・コンポーネント単位のファイル管理で、修正・更新の効率化を行ないました。</p>
   
      <h5 class="point__title">入力チェック</h5>
      <p>お問い合わせフォームでは必須項目が未入力の場合送信ボタンをクリックできないよう実装しました。</p>

      <h5 class="point__title">Swiperスライダー</h5>
      <p>トップページのギャラリースライダーはSwiperを利用。<br>
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
  .point__box {
    display: flex;
    gap: 30px;
    align-items: center;
    margin-bottom: 30px;
    @include sp {
      display: block;
    }
    img {
      width: 40%;
      @include sp {
        width: 100%;
      }
    }
    p {
      width: 40%;
      @include sp {
        width: 100%;
      }
    }
  }

  .afterURL {
    transform: translateY(-20px);
  }
</style>
