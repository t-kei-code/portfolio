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
      全体のSCSS設計はBEMに従い、保守性を意識しました。<br>
      変数定義と、コンポーネントごとのファイル分割によって効率的に修正を行えるよう意識しました。<br>
      「お問い合わせ」フォームでは入力チェックを行い、必須項目がすべて入力されていないとsubmitボタンをクリックできないよう実装しました。
      <img src="/public/image 34.png" alt="" srcset="">
    </template>
  </WorkDetailLayout>
</template>
