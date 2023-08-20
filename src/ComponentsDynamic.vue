<script setup lang="ts">
import { ref } from 'vue';
import Input from './components/Input.vue';
import Select from './components/Select.vue';
import Radio from './components/Radio.vue';

const currentComp = ref(Input);
const currentCompName = ref("Input");

const compList = [Input, Radio, Select];
const compNameList: string[] = ["Input", "Radio", "Select"];

let currentCompIndex = 0;

const switchConmp = (): void => {
  currentCompIndex++;
  if(currentCompIndex >= 3) {
    currentCompIndex = 0;
  }
  currentComp.value = compList[currentCompIndex];
  currentCompName.value = compNameList[currentCompIndex];
}

</script>

<template>
  <p>コンポーネント名：{{ currentCompName }}</p>
  <KeepAlive>
    <component v-bind:is="currentComp" />
  </KeepAlive>
  <button v-on:click="switchConmp">切り替え</button>
</template>

<style>
  .box {
    border: 1px solid green;
    margin: 10px;
  }
</style>

