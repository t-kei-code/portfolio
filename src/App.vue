<script setup>
import { RouterLink, RouterView, useRoute } from 'vue-router'
import { ref, onMounted, onUnmounted } from 'vue'
import ParticleBg from './components/canvas/ParticleBg.vue'
import WaveAnimation from './components/canvas/WaveAnimation.vue'

const route = useRoute()
const isScrolled = ref(false) // スクロール状態を管理

const handleScroll = () => {
  isScrolled.value = window.scrollY > window.innerHeight
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header :class="{ on: isScrolled }">
    <!-- <ul>
      <li class="header__item header__logo">
        <RouterLink to="/">Kei Tsukamoto</RouterLink>
      </li>
    </ul> -->
    <ul class="header__list">
      <li class="header__item"><RouterLink to="/">Top</RouterLink></li>
      <li class="header__item"><RouterLink to="/#works">Works</RouterLink></li>
      <li class="header__item"><RouterLink to="/about">About</RouterLink></li>
    </ul>
  </header>

  <main>
    <ParticleBg v-if="route.name !== 'works'"></ParticleBg>
    <WaveAnimation v-if="route.name !== 'works'"></WaveAnimation>

    <RouterView />
  </main>
  <footer>
    <p>footerテキストfooterテキストfooterテキストfooterテキストfooterテキスト</p>
  </footer>
</template>

<style lang="scss">
* {
  list-style: none;
  text-decoration: inherit;
  margin: 0;
  padding: 0;
  scroll-behavior: smooth;
}
a {
  text-decoration: none;
  color: inherit;
}

html,
body {
  overflow-x: hidden;
  font-family: 'Zen Kaku Gothic New', serif;
  font-weight: 400;
  width: 100%;
  overflow-x: hidden;
  line-height: 1.2;
  list-style: none;
}

header {
  width: 100%;
  position: fixed;
  top: 0;
  right: 0;
  z-index: 100;
  color: aliceblue;
  display: flex;
  background-color: transparent;
  transition:
    background 0.3s,
    box-shadow 0.3s;

  .header__list {
    display: flex;
    justify-content: space-around;
    width: 40%;
    margin-left: auto;
  }

  .header__item {
    font-size: 1.5rem;
    padding: 10px;
  }

  .header__logo {
    font-size: 1.7rem;
    padding-left: 30px;
  }
}

/* スクロール時のスタイル */
header.on {
  color: rgba(0, 0, 0, 0.8);
}

/* ////footer///// */
footer {
  background-color: rgb(74, 74, 83);
  color: white;
  text-align: center;
  padding: 100px 0;
}
</style>
