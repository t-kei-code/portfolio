<script setup>
import ThreeGallary from '@/components/three-gallary/ThreeGallary.vue';
import WorksList from '@/components/WorksList.vue'
import { Swiper, SwiperSlide } from "swiper/vue"
import { Pagination, Navigation} from "swiper/modules"
import "swiper/css";
import 'swiper/css/pagination'
import 'swiper/css/navigation'

const videos = [
  { src: "/Ripple.mp4", link: "https://im-t-kei-ripple-effect.netlify.app/"},
  { src: "/Ripple.mp4", link: "https://im-t-kei-ripple-effect.netlify.app/"},
  { src: "/Ripple.mp4", link: "https://im-t-kei-ripple-effect.netlify.app/"},
  { src: "/Ripple.mp4", link: "https://im-t-kei-ripple-effect.netlify.app/"},
  { src: "/Ripple.mp4", link: "https://im-t-kei-ripple-effect.netlify.app/"},
  { src: "/Ripple.mp4", link: "https://im-t-kei-ripple-effect.netlify.app/"},
]
</script>

<template>
  <section class="tentative">
    ※パフォーマンスやスマートフォン表示に関する問題があり、現在も修正作業を進めています。
  </section>

  <section id="about" class="about">
    <h2 class="section__title">
      <p class="section__title--en">私について</p>
      <p class="section__title--jp">About</p>
    </h2>

    <div class="about__container">
      <div class="about__img">
        <img src="/public/aboutMe.png" alt="" />
      </div>
      <div class="about__text">
        <ul class="about__list">
          <li class="about__item">Kei Tsukamoto</li>
          <li class="about__item">塚本 渓</li>
          <li class="about__item">
            1998年生まれ、京都府出身。現在は就労移行支援に通い、コーダーとしての就職を目指して学習中です。<br>
            基本的なサイトのコーディングに加え、Three.jsなどを使った演出やインタラクティブな表現、デザインにも幅広く取り組んでいます。    
          </li>
          <li class="about__item">
            <button class="about__btn"><RouterLink to="/about">View Profile</RouterLink></button>
          </li>
        </ul>
      </div>
    </div>
  </section>

  <section id="lead" class="lead">
    <h2 class="section__title">
      <p class="section__title--en">できること</p>
      <p class="section__title--jp">Skill</p>
    </h2>
    <div class="lead__container">
      <ul class="lead__list">
        <li class="lead__item">
          <p class="lead__item-title"> コーディング</p>
          <p class="lead__item-text">デザインカンプに忠実なマークアップが可能です。レスポンシブ対応やBEM設計にも対応します。</p>
          <p class="lead__item-skill">HTML / SCSS / Javascript / jQuery / WordPress / Vue.js /</p>
        </li>
        <li class="lead__item">
          <p class="lead__item-title"> デザイン</p>
          <p class="lead__item-text">既存素材の簡単な加工、画像補正、LPやバナーの制作が可能です。<br>コーダー視点で「実装しやすいデザイン」を意識しています。</p>
          <p class="lead__item-skill">Illustrator / Photoshop / Figma</p>
        </li>
        <li class="lead__item">
          <p class="lead__item-title"> インタラクション・3D表現</p>
          <p class="lead__item-text">JavaScript や Three.js を用いたアニメーション・WebGL表現を学習しています。3Dモデルの表示やアニメーション表現をポートフォリオサイト内で試しています。</p>
          <p class="lead__item-skill">Three.js / GSAP / Blender</p>
        </li>
      </ul>
    </div>
  </section>

  <section id="works" class="works">
    <div class="works__inner">
      <h2 class="section__title">
        <p class="section__title--en">制作物</p>
        <p class="section__title--jp">Works</p>
      </h2>
      <div class="works__container">
        <WorksList></WorksList>
      </div>
    </div>
  </section>

  <section class="works-three">
    <h2 class="section__title works-three__title">
      <p class="section__title--en">3D・インタラクション</p>
      <p class="section__title--jp">3D/interraction</p>
    </h2>
    <div class="works__container">
      <Swiper 
        class="works-three__slider"
        :space-between="30"
        :slidesPerView="4"
        :loop="true"
        :pagination="{ clickable: true}"
        :navigation="true"
        :modules="[Pagination, Navigation]"
        >
        <SwiperSlide v-for="(video, i) in videos" :key="i" class="works-three__item">
          <a :href="video.link" target="_blank" rel="noopener">
            <video :src="video.src" autoplay muted loop playsinline style="width: 100%; height: 100%; object-fit: cover;"></video>
          </a>
        </SwiperSlide>
    </Swiper>
  </div>
  </section>
</template>

<style scoped lang="scss">
@use "@/styles/mixin" as *;
.mv {
  position: relative;
  top: 0;
  left: 0;

  &__title {
  position: absolute;
  top: 50%;
  left: 25%;
  transform: translate(-50%, -50%);
  color: white;
  font-family: "Noto Serif JP", serif;
  font-weight: 400;
  font-size: clamp(3rem, 2.648rem + 1.5vw, 4rem);
  pointer-events: none;
  @include sp {
    left: 35%;
  }
}
}

/* section */
.section__title {
  font-weight: bold;
  font-size: 1.5rem;
  color: #7b6758;
  margin-bottom: 30px;
  text-align: left;
  border-bottom: solid #7b6758 1px;

  &--en {
  font-size: 0.8rem;
  }
  &--jp {
    padding-bottom: 4px;
  }
}

.tentative {
   margin-top: 30px;
  padding: 0 5%;
  max-width: 1400px;
  margin: 30px auto 0;
  text-align: center;
}


/* ////section__about//// */
#about {
  margin-top: 30px;
  padding: 0 5%;
  max-width: 1400px;
  margin: 30px auto 0;
}

.about__container {
  display: flex;
  justify-content: space-between;
  align-items: center;

  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  @include sp {
    display: block;
  }
}

.about__img {
  width: 40%;
  height: auto;
  @include sp {
    width: auto;
  }
}
.about__img img {
  width: 100%;
  height: auto;
  object-fit: cover;
}

.about__text {
  width: 50%;
  line-height: 1.8;
  @include sp {
    width: auto;
  }
}

.about__item:nth-of-type(1) {
  font-size: 0.7rem;
}
.about__item:nth-of-type(2) {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.about__item:nth-of-type(4) {
  display: flex;
  justify-content: flex-end;
}
.about__btn {
  margin-top: 10px;
  position: relative;
  &::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 1px;
    background: $brown;
    transition: width 0.3s ease;
  }

  &:hover::after {
    width: 100%;
  }
}

/*//////////////// section__lead ///////////////////*/
.lead {
  padding: 0 5%;
  max-width: 1400px;
  margin: 30px auto 0;
  &__container {
  max-width: 800px;
  margin: 50px auto;
  color: #787069;
  }

  &__list {
    display: flex;
    justify-content: center;
    gap: 5%;
    @include sp {
      display: block;
    }
  }
  &__item {
    width: 33.3%;
    border: solid 1px #787069;
    border-radius: 10px;
    padding: 20px 10px;
    @include sp {
      width: 100%;
      margin-bottom: 30px;
       padding: 20px 10%;
    }
    &-title {
      font-weight: bold;
      margin-bottom: 10px;
      text-align: center;
    }
    &-text {
      border-bottom: solid 1px #787069;
      padding-bottom: 10px;
    }
    &-skill {
      margin-top: 10px;
    }
  }
}

.lead__text {
  font-size: clamp(1rem, 0.912rem + 0.38vw, 1.25rem);
  line-height: 1.8;
  color: #555;
}
/* フェードインアニメーション */
.fade-in {
  opacity: 0;
  transform: translateY(20px);
  animation: fadeIn 1s ease-out forwards;
}
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* section__work*/
.works {
  padding-top: 30px;
  padding-bottom: 30px;
  background-color: rgb(235, 232, 232);
  &__inner {
    padding: 0 5%;
    max-width: 1400px;
    margin: 30px auto 0;
  }
}

.works__container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

.works-three {
  padding: 0 5%;
  max-width: 1400px;
  margin: 30px auto 0;
   &__container {
  max-width: 800px;
  margin: 50px auto;
  color: #787069;
  }
  &__title {
    
  }
  &__item {
    width: 30%;
    height: 250px;
    padding-top: 30px;
    padding-bottom: 30px;
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
}

</style>
