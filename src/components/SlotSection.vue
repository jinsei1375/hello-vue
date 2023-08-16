<script setup lang="ts">

interface Props {
  name: string
}
defineProps<Props>();

</script>

<template>
  <section class="box">
    <h1>{{ name }}さんの状況</h1>
    <slot>
      <p>{{ name }}は問題ありません</p>
    </slot>
  </section>
</template>

<style>
  .box {
    border: 1px solid green;
    margin: 10px;
  }
</style>

