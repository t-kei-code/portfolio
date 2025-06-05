<script setup>
defineProps({
  category: String,
  title: String,
  url: String,
  image: String,
  content: String,
  tasks: String,
  tech: String,
  duration: String,
})
const baseURL = import.meta.env.BASE_URL
</script>

<template>
  <div class="container">
    <p class="work__category">{{ category }}</p>
    <h3 class="work__title">{{ title }}</h3>
    <a class="work__url" :href="url" target="_blank">{{ url }}</a>
    <slot name="afterUrl"></slot>
    <img class="work__img" :src="baseURL + image" :alt="title" />

    <div class="content__box">
      <div class="box--side">
        <ul class="detail__list">
          <li>
            <h5 class="detail__title">担当内容</h5>
            <p>{{ tasks }}</p>
          </li>
          <li>
            <h5 class="detail__title">使用技術</h5>
            <p>{{ tech }}</p>
          </li>
          <li>
            <h5 class="detail__title">制作期間</h5>
            <p>{{ duration }}</p>
          </li>
          <li>
            <h5 class="detail__title">概要</h5>
            <p><slot name="summary"></slot></p>
          </li>
          <li>
            <h5 class="detail__title">工夫した点</h5>
            <p><slot name="point"></slot></p>
          </li>
        </ul>
      </div>
    </div>
  </div>

  <div>
    <RouterLink to="/#works"><button class="back__btn">作品一覧に戻る</button></RouterLink>
  </div>
</template>

<style scoped lang="scss">
@use "@/styles/mixin" as *;

.work__category {
  margin-bottom: 10px;
}

.work__title {
  margin-bottom: 10px;
  font-weight: bold;
  font-size: 1.5rem;
}

.work__url {
  margin-bottom: 30px;
  display: inline-block;
  border-bottom: solid $gray 1px;
}

.work__img {
  width: 100%;
  max-width: 800px;
  height: 500px;
  object-fit: contain;
  display: block;
  margin: 0 auto;
  @include sp {
    width: 100%;
    height: auto;
    object-fit: contain;
  }
}

.content__box {
  margin: 80px auto 0;
  width: 100%;
  max-width: 1100px;
  @include sp {
    display: block;
      margin: 40px auto 0;
  }

  .box--side {
    width: 100%;
    @include sp {
      width: 100%;
    }
  }
  .box--main {
    width: 80%;
    @include sp {
      width: 100%;
    }
  }

  .detail__list {
    width: 100%;
    li {
      display: flex;
      justify-content: space-between;
      margin-bottom: 48px;
      @include sp {
        margin-bottom: 36px;
        display: block;
      }
    }
    p {
      width: 80%;
      @include sp {
        width: 100%;
      }
    }
  }

  .detail__title {
    font-weight: bold;
    font-size: 1.1rem;
    @include sp{
      margin-bottom: 18px;
    }
  }
}

.back__btn {
  margin: 0 auto 50px;
  display: block;
  padding: 10px;
  border: solid $brown 1px;
  border-radius: 8px;

  transition: all 0.3s ease;
    &:hover {
      transform: translateY(-3px);
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    }
}
</style>
