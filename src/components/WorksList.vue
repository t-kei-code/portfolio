<script setup>
import { RouterLink } from 'vue-router'
const baseURL = import.meta.env.BASE_URL

const works = [
  {
    id: 'work01',
    title: '合同会社Work ホームページ',
    category: 'デザイン/コーディング/wordpres化',
    occupation: 'クライアントワーク',
    image: 'work.png',
  },
  {
    id: 'work02',
    title: 'KEI TSUKAMOTOポートフォリオサイト',
    category: 'デザイン/コーディング',
    occupation: '個人製作',
    image: 'portfolio.png',
  },
  // {
  //   id: 'work03',
  //   title: 'work3',
  //   category: 'デザイン/コーディング',
  //   occupation: 'クライアントワーク',
  //   image: '/mockup.jpg',
  // },
  {
    id: 'work04',
    title: 'たいよう保育園 LP',
    category: 'デザイン/コーディング',
    occupation: '課題',
    image: 'taiyo.png',
  },
  {
    id: 'work05',
    title: 'SPORTHERE LP',
    category: 'コーディング',
    occupation: '課題',
    image: 'sport.png',
  },
  {
    id: 'work06',
    title: 'イタリアンレストランSHU LP',
    category: 'デザイン',
    occupation: '課題',
    image: 'food.png',
  },
  {
    id: 'work07',
    title: 'レンタルカメラサービス バナー',
    category: 'デザイン',
    occupation: '課題',
    image: 'camera.png',
  },
  {
    id: 'work08',
    title: '準備中',
    category: 'デザイン',
    occupation: '課題',
    image: '',
  },
]
</script>

<template>
  <ul class="works__list">
    <li class="works__item" v-for="work in works" :key="work.id">
      <RouterLink :to="`/works/${work.id}`">
        <img class="works__img" :src="baseURL + work.image" alt="" />
      </RouterLink>
      <h3 class="works__title">{{ work.title }}</h3>
      <p class="works__category">{{ work.category }}</p>
      <p class="works__occupation">{{ work.occupation }}</p>
    </li>
  </ul>
</template>

<style scoped>
.works__list {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}

.works__item {
  width: calc(45% - 20px);
  margin-bottom: 30px;
  font-size: 0.8rem;
}
.works__img {
  object-fit: contain;
  width: 100%;
  height: 250px;
  border-radius: 3px;
  /* box-shadow: 2px 2px 2px 2px rgba(161, 161, 161, 0.35);
  background-color: rgb(245, 245, 245); */
}
</style>
