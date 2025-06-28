<script setup>
import { onMounted } from 'vue';

onMounted(() => {
  document.querySelectorAll('.skill__name').forEach(function(el){
    // いったん全部閉じる
    function closeAll() {
      document.querySelectorAll('.skill__inline-skill').forEach(d=>d.classList.remove('open'));
    }
    // クリック
    el.addEventListener('click', function(e){
      closeAll();
      const parent = el.closest('.skill__inline-skill');
      if (parent) parent.classList.toggle('open');
      e.stopPropagation();
    });
    // hover（PCのみ）
    el.addEventListener('mouseenter', function(){
      closeAll();
      const parent = el.closest('.skill__inline-skill');
      if (parent) parent.classList.add('open');
    });
    el.addEventListener('mouseleave', function(){
      const parent = el.closest('.skill__inline-skill');
      if (parent) parent.classList.remove('open');
    });
  });
  // 外クリックで閉じる
  document.body.addEventListener('click', function(){
    document.querySelectorAll('.skill__inline-skill').forEach(function(d){
      d.classList.remove('open');
    });
  });
});
</script>

<template>
  <!-- <AboutTextParticle></AboutTextParticle> -->
  <section id="about">
    <div class="about__container">
      <div class="about__img">
        <img src="/public/aboutMe.png" alt="" />
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
  
  <section id="skill" class="skill">
    <h2 class="section__title">
      <p class="section__title--en">スキル</p>
      <p class="section__title--jp">Skill</p>
    </h2>
    <div class="skill__container">
      <ul class="skill__list">
        <!-- コーディング -->
        <li class="skill__item">
          <h3 class="skill__title">コーディング</h3>
          <div class="skill__inline-list">
            <span class="skill__inline-skill">
              <span class="skill__name">HTML(2年)</span>
              <span class="skill__detail">セマンティックなマークアップを意識したHTMLコーディングが可能。</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">CSS,SCSS(2年)</span>
              <span class="skill__detail">BEM設計やSCSSによる効率的なスタイリング設計が得意。</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">JavaScript(1年)</span>
              <span class="skill__detail">DOM操作・ES6記法・バニラJSでの簡易なUI実装が可能。</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">jQuery(6カ月)</span>
              <span class="skill__detail">動的なUIの実装や、フォームのバリデーション、スムーズなアニメーション表現などの経験あり。</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">Vue.js(1.5カ月)</span>
              <span class="skill__detail">コンポーネント化、リアクティブなデータ連携など基本操作が可能。</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">WordPress(1.5か月)</span>
              <span class="skill__detail">WordPressテーマ作成経験あり。</span>
            </span>
          </div>
        </li>
        <!-- デザイン -->
        <li class="skill__item">
          <h3 class="skill__title">デザイン</h3>
          <div class="skill__inline-list">
            <span class="skill__inline-skill">
              <span class="skill__name">Illustrator(6カ月)</span>
              <span class="skill__detail">簡単な画像編集や図形作成、バナー・アイコン制作などの基本操作が可能</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">Photoshop(6カ月)</span>
              <span class="skill__detail">簡単な写真加工、色調補正など可能。</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">Figma(5カ月)</span>
              <span class="skill__detail">Webデザインカンプやワイヤーフレーム作成が可能。</span>
            </span>
          </div>
        </li>
        <!-- インタラクション・3D表現 -->
        <li class="skill__item">
          <h3 class="skill__title">インタラクション・3D表現</h3>
          <div class="skill__inline-list">
            <span class="skill__inline-skill">
              <span class="skill__name">Three.js(6カ月)</span>
              <span class="skill__detail">3Dモデル表示や簡単なパーティクル表現、シェーダーのカスタマイズ経験あり。</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">GSAP(1カ月)</span>
              <span class="skill__detail">アニメーションUI演出や、ページトランジションの実装経験。</span>
            </span>/
            <span class="skill__inline-skill">
              <span class="skill__name">Blender(2カ月)</span>
              <span class="skill__detail">簡単な3Dモデリング、GLB形式のエクスポートやWeb用素材制作。</span>
            </span>
          </div>
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

#about {}

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
  &__container {
    width: 100%;
    display: flex;
    justify-content: space-between;
    @media (max-width: 900px) {
      display: block;
    }
  }
  &__list {
    width: 100%;
    display: flex;
    justify-content: space-between;
    padding: 0;
    margin: 0;
    list-style: none;
    @media (max-width: 900px) {
      flex-direction: column;
      gap: 36px 0;
    }
  }
  &__item {
    width: 31.5%;
    min-width: 180px;
    @media (max-width: 900px) {
      width: 100%;
      margin-bottom: 32px;
    }
  }
  &__title {
    font-weight: bold;
    color: #5a5248;
    font-size: 1.2rem;
    margin-bottom: 8px;
  }
  &__inline-list {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    gap: 0 0.3em;
    font-size: 1em;
    color: #676767;
    line-height: 2;
    @media (max-width: 900px) {
      line-height: 2.1;
    }
  }
  &__inline-skill {
    position: relative;
    display: inline-block;
  }
  &__name {
    cursor: pointer;
    border-bottom: 1px dotted $brown;
    transition: color 0.15s;
    &:hover,
    &.active {
      color: $brown;
    }
  }
  &__detail {
    display: none;
    position: absolute;
    left: 0;
    top: 1.8em;
    z-index: 10;
    background: #fff;
    border: 1px solid #e6e3e0;
    border-radius: 8px;
    padding: 0.8em 1em;
    box-shadow: 0 2px 16px #0002;
    font-size: 0.95em;
    min-width: 190px;
    max-width: 280px;
    white-space: pre-line;
    @include sp {
      min-width: 140px;
      font-size: 0.96em;
    }
  }
  &__inline-skill.open &__detail {
    display: block;
    animation: fadeIn 0.18s;
  }
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(12px);}
    to   { opacity: 1; transform: translateY(0);}
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
  color: rgb(126, 114, 114);
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
