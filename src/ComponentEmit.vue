<script setup lang="ts">
import { ref } from 'vue';
import OneSectionEmit from './components/OneSectionEmit.vue';

const randInit = Math.round(Math.random() * 10);
const rand = ref(randInit);
const onCreateNewRand = (): void => {
  rand.value = Math.round(Math.random() * 10);
}
</script>

<template>
  <section>
    <p>親コンポーネントで乱数を表示：{{ rand }}</p>
    <OneSectionEmit
      v-bind:rand="rand"
      v-on:CreateNewRand="onCreateNewRand" />
  </section>
</template>

<style>
  section {
    border: 1px solid blue;
    margin: 10px;
  }
</style>
