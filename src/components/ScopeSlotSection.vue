<script setup lang="ts">
import { reactive } from 'vue';

const memberInfo = reactive({
  name: "田中太郎",
  state: "問題ありません"
});

</script>

<template>
  <section>
    <slot v-bind:memberInfo="memberInfo">
      <h1>{{ memberInfo.name }}</h1>
      <p>{{ memberInfo.state }}</p>
    </slot>
  </section>
</template>

<style>
  .box {
    border: 1px solid green;
    margin: 10px;
  }
</style>

