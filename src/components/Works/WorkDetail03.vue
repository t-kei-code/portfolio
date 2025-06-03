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
      <div class="point__box">
        <img src="/public/image 35.png" alt="" srcset="">
        <p>全体のSCSS設計はBEMに従い、保守性を意識しました。</p>
      </div>
      <div class="point__box">
        <img src="/public/image 34.png" alt="" srcset="">
        <p>SCSSファイルをページや共通パーツごとに分割し、管理や再利用しやすい設計に</p>
      </div>
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
