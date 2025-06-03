<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'たいよう保育園 LP',
  url: 'https://cottleya.jobtra-itweb.com/taiyo-preschool/',
  image: 'taiyo.png',
  tasks: 'デザイン/コーディング/',
  tech: 'html, css',
  duration: '1ヶ月',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
  <template #summary>
      たいよう保育園(架空)開所に伴い、ホームページのデザインとコーディングを行いました。
    </template>
    <template #point>
      <p>
        かわいらしさを大切にしながらも、シンプルで洗練されたおしゃれな印象を目指しました。<br>
        メインビジュアルでは明朝体を採用し、キャッチコピーは縦書きで配置することで、上品さと独自性を演出しています。
      </p>
      <p>コーディング：全体のSCSS設計はBEMに従い、保守性を意識しました。</p>
    </template>
  </WorkDetailLayout>
</template>
