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

  <section id="lead">
    <div class="lead__container">
      <h2 class="lead__title">「デザイン × コードで、より自由な表現を。」</h2>
      <p class="lead__text">
        視覚的なデザインだけでなく、コーディングを活かした表現にも挑戦しています。<br />
        基本的なコーディング業務に対応しつつ、インタラクティブな演出や機能美を意識したデザインの実装にも取り組んでいます。<br />
        静的なデザインから動きのある演出まで、柔軟に対応します。
      </p>
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

  <section id="about">
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
  font-size: clamp(3rem, 2.648rem + 1.5vw, 4rem);
  pointer-events: none;
  @include sp {
    left: 35%;
  }
}
}

/*//////////////// section__lead ///////////////////*/
.lead__container {
  text-align: center;
  max-width: 800px;
  margin: 50px auto;
  color: #787069;
}
.lead__title {
  font-size: clamp(1.5rem, 1.324rem + 0.75vw, 2rem);
  font-weight: bold;
  letter-spacing: 0.05em;
  margin-bottom: 15px;
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

/* section */
section {
  padding: 30px 5%;
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

/* section__work*/
#works {
  background-color: rgb(235, 232, 232);
}

.works__container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

/* ////section__about//// */
#about {
}

.about__container {
  display: flex;
  justify-content: space-between;
  align-items: center;

  width: 100%;
  margin: 0 auto;
}

.about__img {
  width: 35%;
  height: auto;
}
.about__img img {
  width: 100%;
  height: auto;
  object-fit: cover;
}

.about__text {
  width: 50%;
  line-height: 1.8;
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
}
</style>
