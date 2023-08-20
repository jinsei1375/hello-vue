<script setup lang="ts">
import { ref } from 'vue';
import SlotSection from './components/SlotSection.vue'

const taroProblemsInit: string[] = ["電話が通じません。", "留守です."];
const taro = ref("田中たろう");
const taroProblems = ref(taroProblemsInit);
const jiro = ref("山田次郎");



</script>

<template>
  <section>
    <h2>Slotの利用</h2>

    <!-- Slotを利用する際はコンポーネントの開始タグと終了タグが必要 -->
    <SlotSection v-bind:name="taro">
      <template v-slot:detail>
        <ul>
          <li v-for="problem in taroProblems" v-bind:key="problem">
            {{ problem }}
          </li>
        </ul>
      </template>
      <template v-slot:default>
        <p>問題発生</p>
      </template>
    </SlotSection>
    <SlotSection v-bind:name="jiro">
    <template v-slot:default>
        <p>微妙な問題発生</p>
      </template></SlotSection>
  </section>
</template>

<style>
  .box {
    border: 1px solid green;
    margin: 10px;
  }
</style>

