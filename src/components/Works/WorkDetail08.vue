<script setup>
import WorkDetailLayout from '@/components/WorkDetailLayout.vue'

const workData = {
  category: '課題',
  title: 'レンタルカメラサービス バナー',
  image: 'camera.png',
  tasks: 'デザイン/',
  tech: 'Illustrator, Photoshop',
  duration: '20日',
}
</script>

<template>
  <WorkDetailLayout v-bind="workData">
     <template #summary>
        レンタルカメラサービスCamerenの販促バナーを制作しました。
      </template>
      <template #point>
        <p>バナーそれぞれのペルソナを以下に設定。</p>
        <h5 class="point__title">①カメラマニア層</h5>
        <p>
          カメラのガジェットとしての部分に特に魅力を感じ、カメラ収集事態を趣味としている。<br>
          試してみたい機種は多いが金銭的にも現実的ではない。
        </p>
        <p>メインカラーはワインレッドを選定し、落ち着きと高級感を表現しました。<br>
          またカメラの写真を多用し、レンタル機種の多さがぱっと見で伝わるよう意識しました。
        </p>

        <h5 class="point__title"> ②ファミリー層</h5>
        <p>
          本格的なカメラに興味はあるものの、種類や性能については詳しくない。<br>
          いきなり高額なカメラを購入するのはハードルが高い。
        </p>
        <p>
          ライト層をターゲットに設定し、フォントや配色で親しみやすい印象を目指しました。<br>
          また人物が映っているイベントの写真を多く選定し、カメラよりもカメラの使用シーンのイメージがつきやすいよう意識しました。
        </p>
      </template>
  </WorkDetailLayout>
</template>

<style lang="scss" scoped>
  p {
    margin-bottom: 10px;
  }
</style>
