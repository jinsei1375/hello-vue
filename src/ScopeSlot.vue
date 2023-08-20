<script setup lang="ts">

import ScopeSlotSection from './components/ScopeSlotSection.vue'
</script>

<template>
  <section>
    <ScopeSlotSection>
      <template v-slot:default="slotProps">
        <dl>
          <dt>名前</dt>
          <dd>{{ slotProps.memberInfo.name }}</dd>
          <dt>状況</dt>
          <dd>{{ slotProps.memberInfo.state }}</dd>
        </dl>
      </template>
    </ScopeSlotSection>
  </section>
</template>

<style>
  .box {
    border: 1px solid green;
    margin: 10px;
  }
</style>

