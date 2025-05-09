<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: 'クライアントワーク',
  title: '合同会社Work様 - コーポレートサイト',
  url: 'https://go-work.co.jp/',
  image: 'work.png',
  tasks: 'デザイン/コーディング/wordpress化',
  tech: 'html, css(scss), javascript, php',
  duration: '6ヶ月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
    <p>
      合同会社Work様の会社立ち上げにあたり、コーポレートサイトのデザイン、コーディング、wordpressテーマ化を行いました。
    </p>
    <p>
      クライアント様の「写真や動画は自分で作りたい、テキストは自由に変更可能にしてほしい」との要望にお応えするため、
      全ページwordpressテーマ化をし、管理画面から自由にコンテンツを変更できるよう実装しました。
    </p>
  </WorkDetailLayout>
</template>
