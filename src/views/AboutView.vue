<script setup>
// import AboutTextParticle from '@/components/AboutTextParticle.vue'
</script>

<template>
  <!-- <AboutTextParticle></AboutTextParticle> -->
  <section id="about">
    <div class="about__container">
      <div class="about__img">
        <img src="/public/1308734.jpg" alt="" />
      </div>
      <div class="about__text">
        <ul class="about__list">
          <li class="about__item">Kei Tsukamoto</li>
          <li class="about__item">塚本 渓</li>
          <li class="about__item-text">
            1998年生まれ京都府出身で、現在は就労移行支援に通いながらweb制作の勉強を続けています。<br />
            多方面の知識やモダンな技術を積極的に吸収し、デザインも実装も両方できる自走力のあるクリエイターを目指しています。
            javascriptを用いた動きのあるサイトが好きです。 趣味は、ギターとゲームが好きです。
          </li>
        </ul>
      </div>
    </div>
  </section>
  <section id="skill">
    <h2 class="section__title">
      <p class="section__title--en">Skill</p>
      <p class="section__title--jp">スキル</p>
    </h2>
    <div class="skill__container">
      <ul class="skill__list">
        <li class="skill__item">
          <h3 class="skill__title">コーディング</h3>
          <p class="skill__text">
            HTML(2年), CSS,SCSS(2年), JavaScript(1年), jquery(6カ月), Vue.js(1.5カ月)
          </p>
          <p class="item__icon"></p>
        </li>
        <li class="skill__item">
          <h3 class="skill__title">デザイン</h3>
          <p class="skill__text">
            Illusttrator(6カ月), Photoshop(6カ月), Figma(5カ月)
          </p>
          <p class="item__icon"></p>
        </li>
        <li class="skill__item">
          <h3 class="skill__title">インタラクション・3D表現</h3>
          <p class="skill__text">Three.js(6カ月), GSAP(1カ月), Blender(2カ月)</p>
          <p class="item__icon"></p>
        </li>
      </ul>
    </div>
  </section>

  <section>
    <h2 class="section__title">
      <p class="section__title--en">Strengths</p>
      <p class="section__title--jp">強み</p>
    </h2>
    <p>・探求心 ー 新しい技術や分野にも積極的に挑戦し、興味を持ったことを深堀して取り組みます。</p>
    <p>・分析力 ー つまずいた原因を見つけて改善につなげるなど、課題から学ぶ力があります。</p>
    <p>・自走力 ー 自ら調べて試しながら学ぶことが得意で、手を動かしながら理解を深めていきます。</p>
  </section>

  <section>
    <h2 class="section__title">
      <p class="section__title--en">Hindrance</p>
      <p class="section__title--jp">障害について</p>
    </h2>
    <p class="hindrance__lead">障害内容：ADHD(不注意優勢型)、うつ病</p>
    <div class="hindrance">
      <p class="hindrance__title">ADHDについて</p>
        <div class="hindrance__text">
          <p>
            2022年5月に注意欠陥・多動性障害（ADHD）の不注意優勢型と診断を受けました。<br />
            <span>興味・集中の偏り</span>、<span>マルチタスクが苦手</span>、<span>対人場面で疲れやすい</span>といった特性があります。
            タスクの細分化、メモや付箋を活用した視覚的な情報整理、服薬などで自己対処をおこなっています。<br />
          </p>
        </div>

      <div>
        <p class="hindrance__title">配慮事項について</p>
        <p>月に一回、半日間の通院休暇をいただきたいです。</p>
      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
@use "@/styles/mixin" as *;
section {
  padding: 30px 15%;
  @include sp {
    padding-right: 5%;
    padding-left: 5%;
  }
}

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

#about {
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
  width: 35%;
  max-width: 400px;
  margin: 0 auto;
  height: auto;
  @include sp {
    width: 100%;
  }
}
.about__img img {
  width: 100%;
  height: auto;
  object-fit: cover;
}

.about__text {
  width: 50%;
   @include sp {
    width: 100%;
  }
}

.about__item {
  &:nth-last-of-type(1) {
    font-size: 0.7rem;
  }
  &:nth-last-of-type(2) {
    font-size: 1.5rem;
    margin-bottom: 10px;
  }
  &-text {
    line-height: 1.8;
  }
}

.about__item:nth-of-type(4) {
  display: flex;
  justify-content: flex-end;
}
.about__btn {
  padding: 5px 10px;
}

.skill {
    &__list {
      width: 100%;
      display: flex;
      justify-content: space-between;
      @include sp {
        display: block;
      }
    }

    &__item {
      width: 30%;
      margin-bottom: 10px;
      @include sp {
        width: 100%;
      }
    }
    &__title {
      font-weight: bold;
      color: $gray;
    }
    &__text {
      line-height: 1.8;
    }
}

/////障害について
.hindrance {
  margin-bottom: 20px;
  &__title {
  font-weight: bold;
  font-size: 1.2rem;
  color: rgb(88, 88, 88);
  }

  &__lead {
    margin-bottom: 10px;
  }

  &__text {
    line-height: 1.8;
    margin-bottom: 10px;
  }
}

</style>
