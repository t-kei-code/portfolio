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

//loading
const isLoading = ref(true)

onMounted(() => {
  window.addEventListener('scroll', handleScroll)

  //loading
  setTimeout(()=> {
    isLoading.value = false
  }, 3000)
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
  <div class="loading" v-if="isLoading">
  <dotlottie-player src="https://lottie.host/edfa3aa4-0d8c-463c-a101-bdc7defbbeed/szwqbN7QJO.lottie" background="transparent" speed="1" style="width: 300px; height: 300px" loop autoplay></dotlottie-player>
    <p class="loading__text">Loading...</p>
  </div>
  <div class="canvas" :class="{ 'is-about' : route.name === 'about'}" v-if="route.name !== 'works'">
    <ParticleBg ></ParticleBg>
    <WaveAnimation></WaveAnimation>
    <ParticleAnimation v-if="route.name ==='home'"></ParticleAnimation>
    <AboutAnimation v-if="route.name ==='about'"></AboutAnimation>


    <div class="canvas__title">
      <p v-if="route.name === 'home'">Kei Tsukamoto<br />Portfolio</p>
      <p v-else-if="route.name === 'about'">ABOUT</p>
    </div>

    <div class="canvas__scroll-icon">scroll</div>
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
.loading {
  position: fixed;
  inset: 0;
  z-index: 9999;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: white;

  &__text {
    font-size: 1.5rem;
    animation: fade 1.2s ease-in-out infinite;
  }
}
@keyframes fade {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

///////
.canvas {
height: calc(var(--vh, 1vh) * 100);
width: 100%;
position: relative;
overflow: hidden;
transition: height 1s ease;

&.is-about {
    height: calc(var(--vh, 1vh) * 50);
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

  ///////
  &__scroll-icon {
        font-size: clamp(0.75rem, 0.618rem + 0.56vw, 1.125rem);
        font-weight: bold;
        color: rgba(255, 255, 255,0.8);

        position: absolute;
        bottom: 10px;
        left: 50%;
        text-align: center;

            &::after {
            content: "";
            display: block;
            width: 1px;
            height: 55px;
            background-color: rgb(255, 255, 255);
            margin: 8px auto 0;
            animation: scrollLine 1.6s ease-in-out infinite;
            transform-origin: top;
        }

        @keyframes scrollLine {
            0% {
            transform: scaleY(1);
            opacity: 1;
            }
            50% {
            transform: scaleY(0.5);
            opacity: 0.4;
            }
            100% {
            transform: scaleY(1);
            opacity: 1;
            }
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

    @include sp {
      display: none;
      opacity: 0;
      transform: translateY(-20px);
      transition: opacity 0.4s ease, translate 0.4s ease;

      flex-direction: column;
      position: absolute;
      background: white;
      width: 100%;
      height: 100vh;
      text-align: right;
      padding: 16px 32px;
      gap: 20px;
      z-index: 10;
  }

    &.is-open {
    opacity: 1;
    transform: translateY(0);
    z-index: 12;

    display: flex;
    justify-content: center;
    align-items: center;
    color: black;
    // width: 100vw;
    // height: 100vh;
    text-align: center;
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
    position: relative;
    z-index: 11;
  }

  //メニューボタン//
  &__btn {
    display: none;

     width: 56px;
    height: 52px;
    background-color: rgba(255, 255, 255, 0.3);
    position: absolute;
    top: 0;
    right: 0;
    pointer-events: auto;
    z-index: 999;

    @include sp {
      display: block;

      background: rgba(31, 27, 27, 0.4); // 見えやすく
      border: 1px solid rgb(255, 255, 255);

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
