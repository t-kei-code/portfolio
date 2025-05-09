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
        </ul>
      </div>

      <div class="box--main">
        <h4 class="detail__title">概要</h4>
        <slot></slot>
      </div>
    </div>
  </div>

  <div>
    <RouterLink to="/#works"><button class="back__btn">作品一覧に戻る</button></RouterLink>
  </div>
</template>

<style scoped lang="scss">
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
}

.work__img {
  width: 800px;
  height: 500px;
  object-fit: contain;
  display: block;
  margin: 0 auto;
}

.content__box {
  margin-top: 50px;
  display: flex;
  justify-content: space-between;
  gap: 3%;
  width: 100%;

  .box--side {
    width: 35%;
  }
  .box--main {
    width: 65%;
  }

  .detail__list {
    li {
      margin-bottom: 10px;
    }
  }

  .detail__title {
    font-weight: bold;
    font-size: 1.1rem;
  }
}

.back__btn {
  margin: 0 auto 50px;
  display: block;
  padding: 10px;
}
</style>
