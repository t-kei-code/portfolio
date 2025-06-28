<script setup>
import { ref, onMounted } from 'vue'
import { RouterLink } from 'vue-router'

const baseURL = import.meta.env.BASE_URL

const works = [
  { id: 'work01', title: '合同会社Work様 ホームページ', category: 'デザイン/コーディング/WordPress化', occupation: 'クライアントワーク', image: 'work.png' },
  { id: 'work02', title: 'KEI TSUKAMOTO ポートフォリオサイト', category: 'デザイン/コーディング', occupation: '個人製作', image: 'portfolio.png' },
  { id: 'work03', title: '青牡丹工務店 コーポレートサイト', category: 'コーディング', occupation: '課題', image: 'aobotan.png' },
  { id: 'work04', title: 'イタリアンダイニングSHU LP', category: 'デザイン', occupation: '課題', image: 'food.png' },
  { id: 'work05', title: 'たいよう保育園 LP', category: 'デザイン/コーディング', occupation: '課題', image: 'taiyo.png' },
  { id: 'work06', title: 'SPORTHERE LP', category: 'コーディング', occupation: '課題', image: 'sport.png' },
  { id: 'work07', title: '洗顔用化粧水バナー', category: 'デザイン', occupation: '課題', image: 'kesyousui.jpg' },
  { id: 'work08', title: 'レンタルカメラサービス バナー', category: 'デザイン', occupation: '課題', image: 'camera.png' },
]

const worksRef = ref([])
const delays = works.map((_, i) => `${i * 0.2}s`)  // 🔁 キャッシュ済み delay 値
let hasShown = false

onMounted(() => {
  const target = worksRef.value[0]
  const handleScroll = () => {
    if (hasShown) return
    const scrollY = window.scrollY
    const windowHeight = window.innerHeight
    const targetTop = target.offsetTop
    if (scrollY + windowHeight > targetTop + 100) {
      worksRef.value.forEach(el => {
        const inner = el.querySelector('.works__inner')
        if (inner) inner.classList.add('show')
      })
      hasShown = true
      window.removeEventListener('scroll', handleScroll)
    }
  }
  window.addEventListener('scroll', handleScroll)
  handleScroll()
})
</script>

<template>
  <ul class="works__list">
    <li
      v-for="(work, index) in works"
      :key="work.id"
      ref="worksRef"
      class="works__item"
    >
      <div
        class="works__inner"
        :style="{ transitionDelay: delays[index] }"
      >
        <RouterLink :to="`/works/${work.id}`">
          <img
            class="works__img"
            :src="baseURL + work.image"
            :alt="work.title"
          />
        </RouterLink>
        <h3 class="works__title">{{ work.title }}</h3>
        <p class="works__category">{{ work.category }}</p>
        <p class="works__occupation">{{ work.occupation }}</p>
      </div>
    </li>
  </ul>
</template>

<style scoped lang="scss">
@use "@/styles/mixin" as *;

.works {
  &__list {
    display: flex;
    justify-content: center;
    gap: 5%;
    flex-wrap: wrap;

    @include sp {
      display: block;
    }
  }

  &__item {
    width: 50%;
    max-width: 400px;
    margin-bottom: 30px;
    font-size: clamp(0.875rem, 0.831rem + 0.19vw, 1rem);
    border-radius: 10px;
    transition: transform 0.4s ease, box-shadow 0.4s ease;

    &:hover {
      transform: translateY(-4px);
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
    }

    @include sp {
      width: 100%;
      margin: 0 auto 30px;
    }

    .works__inner {
      transition: opacity 0.6s ease, transform 0.6s ease;
      opacity: 0;
      padding: 5px;

      &.show {
        opacity: 1;
        transform: translateY(0);
      }
    }
  }

  &__img {
    object-fit: contain;
    width: 100%;
    height: 250px;
    border-radius: 3px;
  }

  &__title {
    font-weight: bold;
  }

  &__category {
    margin-bottom: 0;
  }
}
</style>
