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
      青牡丹工務店のコーディング
    </template>
    <template #point>
      <div class="point__box">
        <img src="/public/image 35.png" alt="" srcset="">
        <p>全体のSCSS設計はBEMに従い、保守性を意識しました。</p>
      </div>
      <div class="point__box">
        <img src="/public/image 34.png" alt="" srcset="">
        <p>SCSSファイルをページや共通パーツごとに分割し、管理や再利用しやすい設計に</p>
      </div>
      <div class="point__box">
        <p>「お問い合わせ」フォームでは入力チェックを行い、必須項目がすべて入力されていないとsubmitボタンをクリックできないよう実装しました。</p>
      </div>

      <div>
        <p>課題を通して、コーディングの正確さと効率が向上</p>
        <ul>
          <li>・品質チェックシートを用いた修正フローの確立</li>
          <li>・よく使う処理やパーツのコードスニペット化</li>
          <li>・ファイル構造のテンプレート化</li>
        </ul>
      </div>
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
</style>
