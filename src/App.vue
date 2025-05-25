<script setup>
import { RouterLink, RouterView, useRoute } from 'vue-router'
import { ref, onMounted, onUnmounted } from 'vue'
import ParticleBg from './components/canvas/ParticleBg.vue'
import WaveAnimation from './components/canvas/WaveAnimation.vue'
import ParticleAnimation from '@/components/canvas/ParticleAnimation.vue'
import AboutAnimation from './components/canvas/AboutAnimation.vue'

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

const isMenuOpen = ref(false)
const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

</script>

<template>
  <div class="canvas" :class="{ 'is-about' : route.name === 'about'}" v-if="route.name !== 'works'">
      <ParticleBg ></ParticleBg>
      <WaveAnimation></WaveAnimation>
      <ParticleAnimation v-if="route.name ==='home'"></ParticleAnimation>
      <AboutAnimation v-if="route.name ==='about'"></AboutAnimation>


      <div class="canvas__title">
        <p v-if="route.name === 'home'">Kei Tsukamoto<br />Portfolio</p>
        <p v-else-if="route.name === 'about'">ABOUT</p>
      </div>
  </div>

  <header :class="{ on: isScrolled , 'subpage' : route.name !== 'home'}" class="header">
    <ul>
      <li class="header__item header__logo">
        <RouterLink to="/">Kei Tsukamoto</RouterLink>
      </li>
    </ul>

    <ul class="header__list" :class="{ 'is-open': isMenuOpen }">
      <li class="header__item"><RouterLink to="/" @click="isMenuOpen = false">Top</RouterLink></li>
      <li class="header__item"><RouterLink to="/#works" @click="isMenuOpen = false">Works</RouterLink></li>
      <li class="header__item"><RouterLink to="/about" @click="isMenuOpen = false">About</RouterLink></li>
    </ul>
    <div class="header__btn" :class="{ 'is-active': isMenuOpen }" @click="toggleMenu">
      <span></span>
      <span></span>
      <span></span>
    </div>
  </header>

  <main>
    <RouterView />
  </main>
  <footer>
    <p>Kei Tsukamoto Portfolio</p>
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
  color: $gray;
}

/////////////////////////////////////
.canvas {
height: 100vh;
position: relative;
overflow: hidden;
transition: height 1s ease;

&.is-about {
    height: 50vh;
  }

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

  &.subpage {
    color: black;
  }

  &__list {
    display: flex;
    justify-content: space-around;
    width: 40%;
    margin-left: auto;

     &.is-open {
      display: flex;
      color: black;
      width: 100vw;
      height: 100vh;
      text-align: center;
      // メニューの表示スタイル
    }

    @include sp {
      display: none;
      flex-direction: column;
      position: absolute;
      top: 52px;
      right: 0;
      background: white;
      width: 100%;
      text-align: right;
      padding: 16px 32px;
      gap: 20px;
      z-index: 10;
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
