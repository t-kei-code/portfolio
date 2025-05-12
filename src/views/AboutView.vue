<script setup>
import AboutTextParticle from '@/components/AboutTextParticle.vue'
</script>

<template>
  <AboutTextParticle></AboutTextParticle>
  <div class="about">
    <h1>About Page</h1>
  </div>

  <section id="about">
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
            多方面の知識やモダンな技術を積極的に吸収し、デザインも実装も両方できる自走力のあるクリエイターを目指しています。<br />
            javascriptを用いた動きのあるサイトが好きです。 趣味は、ギターとゲームが好きです。
          </li>
        </ul>
      </div>
    </div>
  </section>
  <section id="skill">
    <h2 class="section__title">
      <p class="section__title--en">skill</p>
      <p class="section__title--jp">スキル</p>
    </h2>
    <div class="skill__container">
      <ul class="skill__list">
        <li class="list__item">
          <h3 class="item__title">コーディング</h3>
          <p class="item__text">
            HTML(1年), CSS,SCSS(1年), javascript(6カ月), jquery(6カ月), three.js(6カ月),
            vue.js(1.5カ月)
          </p>
          <p class="item__icon"></p>
        </li>
        <li class="list__item">
          <h3 class="item__title">デザイン</h3>
          <p class="item__text">
            Illusttrator(6カ月), Photoshop(6カ月), Figma(5カ月),Blender(3カ月)
          </p>
          <p class="item__icon"></p>
        </li>
        <li class="list__item">
          <h3 class="item__title">スキル</h3>
          <p class="item__text">スキル内容</p>
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
    <p>・難しいことに挑戦する気概、自走力</p>
    <p>・興味の幅が広い</p>
    <p>・クリエイターソフトに慣れるのが早い</p>
  </section>

  <section>
    <h2 class="section__title">障害について</h2>
    <p class="hindrance__lead">障害内容：ADHD(不注意優勢型)、うつ病</p>
    <div class="hindrance">
      <p class="hindrance__title">ADHDについて</p>
      <p>
        2022年5月に注意欠陥・多動性障害（ADHD）の不注意優勢型と診断を受けました。<br />
        細かい作業や書類の確認でミスが多くなる、一度に複数のことを考えると混乱する、物事を先延ばしにしがち、
        整理整頓や時間管理が苦手などの特性があります。
      </p>
      <p>
        自己対処として、タスクを細分化したリストの作成、メモや付箋を活用した視覚的な情報整理、服薬などを実践しています。<br />
        特に、先延ばしやタスク管理の課題は、これらの対策によって大きな改善を実感しています。
      </p>
    </div>

    <div class="hindrance">
      <p class="hindrance__title">うつ病について</p>
      <p>
        2022年5月にうつ病と診断されました。
        対人不安を感じやすく、評価が下がることや叱責を恐れる傾向があります。
      </p>
      <p>
        1年間の自宅療養を経て、現在は就労移行支援に通いながら、認知行動療法やコミュニケーション研修を受けています。
        また、定期的にジムに通うことで、体調の安定にも努めています。
        その結果、現在は週5日安定して通所を続けられています。
      </p>
    </div>
    <div>
      <p class="hindrance__title">配慮事項について</p>
      <p>月に一回、半日間の通院休暇をいただきたいです。</p>
    </div>
  </section>
</template>

<style scoped lang="scss">
section {
  padding: 30px 15%;
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

#about {
  margin-top: 100vh;
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

.skill__list {
  width: 100%;
  display: flex;
  justify-content: space-between;

  .list__item {
    width: 30%;
  }
}

/////障害について
.hindrance {
  margin-bottom: 20px;
}
.hindrance__title {
  font-weight: bold;
  font-size: 1.2rem;
  color: rgb(88, 88, 88);
}

.hindrance__lead {
  margin-bottom: 10px;
}
</style>
