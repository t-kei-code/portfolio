<script setup>
import ParticleAnimation from '@/components/canvas/ParticleAnimation.vue'
import WorksList from '@/components/WorksList.vue'
</script>

<template>
  <div class="mv">
    <ParticleAnimation></ParticleAnimation>
    <p class="mv__title">
      Kei Tsukamoto<br />
      Portfolio
    </p>
  </div>

  <section id="about" class="about">
    <h2 class="section__title">
      <p class="section__title--en">About</p>
      <p class="section__title--jp">私について</p>
    </h2>

    <div class="about__container">
      <div class="about__img">
        <img src="/public/1308734.jpg" alt="" />
      </div>
      <div class="about__text">
        <ul class="about__list">
          <li class="about__item">Kei Tsukamoto</li>
          <li class="about__item">塚本 渓</li>
          <li class="about__item">
            1998年生まれ京都府出身で、現在は就労移行支援に通いながらweb制作の勉強を続けています。<br />
            デザインも実装も両方できる自走力のあるクリエイターを目指しています。
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
      <p class="section__title--en">Skill</p>
      <p class="section__title--jp">できること</p>
    </h2>
    <div class="lead__container">
      <ul class="lead__list">
        <li class="lead__item">
          <p class="lead__item-title"> コーディング</p>
          <p class="lead__item-text">HTML / SCSS / jQuery を用いて、デザインカンプに忠実なマークアップが可能です。レスポンシブ対応やBEM設計にも対応します。</p>
        </li>
        <li class="lead__item">
          <p class="lead__item-title"> デザイン</p>
          <p class="lead__item-text">Illustrator / Photoshop / Figma を用いたバナー制作や簡単なレイアウト設計が可能です。コーダー視点で「実装しやすいデザイン」を意識しています。</p>
        </li>
        <li class="lead__item">
          <p class="lead__item-title"> インタラクション・3D表現</p>
          <p class="lead__item-text">JavaScript や Three.js を用いたアニメーション・WebGL表現の実装経験があります。ポートフォリオでは 3Dモデルやマウス連動表現を取り入れています。</p>
        </li>
      </ul>
    </div>
  </section>

  <section id="works" class="works">
    <h2 class="section__title">
      <p class="section__title--en">Works</p>
      <p class="section__title--jp">制作物</p>
    </h2>
    <div class="works__container">
      <WorksList></WorksList>
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
section {
  padding: 0 5%;
}

.section__title {
  font-weight: bold;
  font-size: 1.5rem;
  color: #7b6758;
  margin-bottom: 30px;
  text-align: left;

  border-bottom: solid #7b6758 1px;
}
.section__title--en {
  font-size: 0.8rem;
}

/* ////section__about//// */
#about {
  margin-top: 30px;
}

.about__container {
  display: flex;
  justify-content: space-between;
  align-items: center;

  width: 100%;
  margin: 0 auto;
  @include sp {
    display: block;
  }
}

.about__img {
  width: 35%;
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
  padding: 5px 10px;
  margin-top: 10px;
}

/*//////////////// section__lead ///////////////////*/
.lead {
  margin-top: 30px;
  &__container {
  text-align: center;
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
    border: solid 1px #787069;
    border-radius: 10px;
    height: 300px;
    padding: 10px;
    @include sp {
      height: auto;
      margin-bottom: 30px;
    }
    &-title {
      font-weight: bold;
      margin-bottom: 10px;
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
#works {
  padding-top: 30px;
  background-color: rgb(235, 232, 232);
}

.works__container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

</style>
