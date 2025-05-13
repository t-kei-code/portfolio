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
  <header :class="{ on: isScrolled }" class="header">
    <ul>
      <li class="header__item header__logo">
        <RouterLink to="/">Kei Tsukamoto</RouterLink>
      </li>
    </ul>

    <ul class="header__list">
      <li class="header__item"><RouterLink to="/">Top</RouterLink></li>
      <li class="header__item"><RouterLink to="/#works">Works</RouterLink></li>
      <li class="header__item"><RouterLink to="/about">About</RouterLink></li>
    </ul>
    <div class="header__btn">
      <span></span>
      <span></span>
      <span></span>
    </div>
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
@use "@/styles/mixin" as *;

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

.header {
  width: 100%;
  position: fixed;
  top: 0;
  right: 0;
  z-index: 100;
  color: aliceblue;
  font-family: "Noto Serif JP", serif;
  font-weight: 400;

  display: flex;
  background-color: transparent;
  transition:
    background 0.3s,
    box-shadow 0.3s;

  &__list {
    display: flex;
    justify-content: space-around;
    width: 40%;
    margin-left: auto;
    @include sp {
      display: none;
    }
  }

 &__item {
  position: relative;
  font-size: 1.5rem;
  padding-top: 10px;

  &:not(.header__logo)::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 1px;
    background: rgba(255, 255, 255,0.8);
    transition: width 0.3s ease;
  }

  &:hover::after {
    width: 100%;
  }
}


  &__logo {
    font-size: 1.7rem;
    padding-left: 30px;
  }

  //メニューボタン//
  &__btn {
    display: none;
    z-index: 20;

    @include sp {
      display: block;
      width: 56px;
      height: 52px;
      background-color: rgba(255, 255, 255, 0.3);
      position: absolute;
      top: 0;
      right: 0;
      z-index: 20;
      pointer-events: auto;

      span {
        display: block;
        position: absolute;
        width: 32px;
        height: 1px;
        background: white;
        left: 50%;
        transform: translateX(-50%);
        transition: all 0.3s ease;
        &:nth-of-type(1) {
            top: 12px;
        }
        &:nth-of-type(2) {
            top: 24px;
        }
        &:nth-of-type(3) {
            bottom: 12px;
        }
      }

      &.is-active {
        span:nth-of-type(1) {
            transform: translateX(-50%) rotate(45deg);
            top: 24px;
        }
        span:nth-of-type(2) {
            opacity: 0;
        }
        span:nth-of-type(3) {
            transform: translateX(-50%) rotate(-45deg);
            top: 24px;
            bottom: auto;
        }
      }
    }
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
