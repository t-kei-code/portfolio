<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: 'クライアントワーク',
  title: '合同会社Work様 - コーポレートサイト',
  url: 'https://go-work.co.jp/',
  image: 'work.png',
  tasks: 'デザイン(動画、写真選定除く)/コーディング/wordpress化',
  tech: 'html, css(scss), javascript, php',
  duration: '6ヶ月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <template #summary>
      合同会社Work様の会社立ち上げにあたり、コーポレートサイトのデザイン、コーディング、wordpressテーマ化を行いました。<br>
      クライアント様の「写真や動画は自分で作りたい、テキストは自由に変更可能にしてほしい」との要望にお応えするため、
      全ページwordpressテーマ化をし、管理画面から自由にコンテンツを変更できるよう実装しました。
    </template>
    <template #point>
      お知らせページではお客様がwordpressパネルから簡単に記事投稿できる仕組みを実装しました。
      また、新着記事がトップページに自動的に表示されるよう工夫しました。
      <!-- <img src="/public/image 36.png" alt="">
      <img src="/public/image 37.png" alt="">
      <img src="/public/image 39.png" alt="">
      <img src="/public/wp.png" alt="" srcset=""> -->
    </template>
  </WorkDetailLayout>
</template>
