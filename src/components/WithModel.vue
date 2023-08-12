<script setup lang="ts">
import { ref } from 'vue';

const name = ref("名無し");

</script>

<template>
  <section>
    <p>
      {{ name }}さんですね！
    </p>
    <input type="text" v-model="name">
  </section>
</template>

<!-- スタイルブロックを独立させるscope属性　
  data属性が付与されて独立できる -->
<style scoped>
  section {
    border: 1px solid orange;
    margin: 10px;
  }
  
</style>