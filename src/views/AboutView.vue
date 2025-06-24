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
            大学卒業後、ネットワークエンジニアとして勤務していましたが、体調を崩し退職。<br>
            その後、療養期間を経て福祉就労を始める中でHTMLやCSSに出会い、独学でコーディングの学習をスタートしました。<br>
            現在はコーダーとしての就職を目指し、就労移行支援事業所でWEB制作について学んでいます。
          </li>
        </ul>
      </div>
    </div>
  </section>
  <section id="skill">
    <h2 class="section__title">
      <p class="section__title--en">スキル</p>
      <p class="section__title--jp">Skill</p>
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

  <section class="strengths">
    <h2 class="section__title">
      <p class="section__title--en">強み</p>
      <p class="section__title--jp">Strengths</p>
    </h2>
    <p class="strengths__item">・探求心 ー 新しい技術や分野にも積極的に挑戦し、興味を持ったことを深堀して取り組みます。</p>
    <p class="strengths__item">・分析力 ー つまずいた原因を見つけて改善につなげるなど、課題から学ぶ力があります。</p>
    <p class="strengths__item">・自走力 ー 自ら調べて試しながら学ぶことが得意で、手を動かしながら理解を深めていきます。</p>
  </section>

  <section class="future">
    <h2 class="section__title">
      <p class="section__title--en">将来について</p>
      <p class="section__title--jp">Future</p>
    </h2>
    
    <p class="future__title">1年目</p>
    <div class="future__text">
      <p>
        まずは基礎力をしっかりと身につけ、カンプ通りに正確なコーディングを行えることを目指します。<br>
        現場でのルールや仕事の流れを理解し、一つひとつの課題に丁寧に向き合いながら、信頼されるコーダーとして着実に成長していきたいです。
      </p>
    </div>

    <p class="future__title">3年目</p>
    <div class="future__text">
      <p>
        より高度なコーディングや、表現力のあるWebサイト制作にも積極的に挑戦したいと考えています。<br>
        JavaScriptやフロントエンドの技術を深め、自分なりの提案や工夫ができるエンジニアを目指します。<br>
        また、後輩やチームメンバーと協力し、プロジェクト全体のクオリティ向上に貢献していきたいです。
      </p>
    </div>

    <p class="future__title">5年目</p>
    <div class="future__text">
      <p>
        より高度なWeb表現やユーザー体験の設計にも携わり、プロジェクト全体をリードできる存在を目指します。<br>
        チーム内では後輩のサポートや技術共有にも積極的に取り組み、新しい価値を生み出せるエンジニアになることが目標です。<br>
        常に最新技術にアンテナを張り、Web制作の現場で頼られる存在であり続けたいと考えています。
      </p>
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

.strengths {
  &__item {
    margin-bottom: 12px;
  }
}

/////障害について
.future {
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
