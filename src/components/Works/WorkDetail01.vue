<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: 'クライアントワーク',
  title: '合同会社Work様 - コーポレートサイト',
  url: 'https://go-work.co.jp/',
  image: 'work.png',
  tasks: 'デザイン(動画、写真選定除く)/コーディング/WordPress化',
  tech: 'HTML, CSS(SCSS), JavaScript, PHP',
  duration: '6ヶ月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      合同会社Work様の会社立ち上げにあたり、コーポレートサイトのデザイン、コーディング、wordpressテーマ化を担当させていただきました。<br>
    </template>
    <template #point>
      <h5 class="point__title">WordPressテーマ化</h5>
      <p>
        クライアント様の「写真や動画は自分で作りたい、テキストは自由に変更可能にしてほしい」との要望にお応えするため、
        全ページwordpressテーマ化をし、管理画面から自由にコンテンツを変更できるよう実装しました。<br>
        また、お知らせ記事を管理できる投稿機能を実装し、トップページには最新記事のリード文が自動的に反映されるように設計しました。
      </p>
      
      <!-- <img src="/public/image 36.png" alt="">
      <img src="/public/image 37.png" alt="">
      <img src="/public/image 39.png" alt="">
      <img src="/public/wp.png" alt="" srcset=""> -->
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