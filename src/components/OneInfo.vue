<script setup lang="ts">
  interface Props {
    title: string;
    content: string;
    number: number;
  }
  defineProps<Props>();
</script>

<template>
  <section>
    <h4>
      {{ title }}
    </h4>
    <p>
      {{ content }}
      <br>
      {{ number }}
    </p>
  </section>
</template>