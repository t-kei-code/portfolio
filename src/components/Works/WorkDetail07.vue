<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'レンタルカメラサービス バナー',
  image: 'camera.png',
  tasks: 'デザイン/',
  tech: 'illustrator, photoshop',
  duration: '20日',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
     <template #summary>
        レンタルカメラサービスCamerenの販促バナーを制作しました。
      </template>
      <template #point>
        バナーそれぞれのペルソナを以下に設定。<br>
        <p>
          ①カメラマニア層：カメラのガジェットとしての部分に特に魅力を感じ、カメラ収集事態を趣味としている。
          試してみたい機種は多いが金銭的にも現実的ではない。
        </p>
        <p>
          ②ファミリー層：本格的なカメラに興味はあるものの、種類や性能については詳しくない。<br>
          いきなり高額なカメラを購入するのはハードルが高い。
        </p>
      </template>
  </WorkDetailLayout>
</template>
