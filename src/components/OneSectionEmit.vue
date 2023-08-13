<script setup lang="ts">
interface Props {
  rand: number;
}
interface Emits {
  (event: "CreateNewRand"): void;
}

defineProps<Props>();
const emit = defineEmits<Emits>();

const onNewRandButtonClick = (): void => {
  emit("CreateNewRand");
}
</script>

<template>
  <section>
    <p>子コンポーネントで乱数を表示：{{ rand }}</p>
    <button v-on:click="onNewRandButtonClick">新たな乱数を発生</button>
  </section>
</template>