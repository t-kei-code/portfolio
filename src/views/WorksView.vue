<script setup>
import { useRoute } from 'vue-router'
import WorkDetail01 from '@/components/Works/WorkDetail01.vue'
import WorkDetail02 from '@/components/Works/WorkDetail02.vue'
import WorkDetail03 from '@/components/Works/WorkDetail03.vue'
import WorkDetail04 from '@/components/Works/WorkDetail04.vue'
import WorkDetail05 from '@/components/Works/WorkDetail05.vue'
import WorkDetail06 from '@/components/Works/WorkDetail06.vue'
import WorkDetail07 from '@/components/Works/WorkDetail07.vue'
import WorkDetail08 from '@/components/Works/WorkDetail08.vue'
const route = useRoute()
const workId = route.params.id

const works = {
  work01: WorkDetail01,
  work02: WorkDetail02,
  work03: WorkDetail03,
  work04: WorkDetail04,
  work05: WorkDetail05,
  work06: WorkDetail06,
  work07: WorkDetail07,
  work08: WorkDetail08,
}

const SelectedComponent = works[workId]
</script>

<template>
  <div class="container">
    <h2 class="section__title">
      <p class="section__title--en">Works</p>
      <p class="section__title--jp">制作物</p>
    </h2>
    <component :is="SelectedComponent" v-if="SelectedComponent" />
  </div>
</template>

<style scoped lang="scss">
@use "@/styles/mixin" as *;

.container {
  background-color: rgb(235, 232, 232);
  padding: 100px 5%;
  @include sp {
    padding: 100px 5% 40px;
  }
}

.section__title {
  text-align: center;

  font-weight: bold;
  font-size: 1.5rem;
  color: #7b6758;
  padding-bottom: 10px;
  margin-bottom: 30px;
  border-bottom: solid #7b6758 1px;
}

.section__title--en {
  font-size: 0.8rem;
}
</style>
