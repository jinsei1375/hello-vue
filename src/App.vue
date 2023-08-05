<script setup lang="ts">
import { ref, computed, reactive } from 'vue'

const name = ref("田中太郎");

const now = new Date();
const nowStr = now.toLocaleTimeString();

let timeStr = nowStr; // リアクティブでない変数として宣言

const timeStrRef = ref(nowStr);

function changeTime(): void {
  const newTime = new Date();
  const newTimeStr = newTime.toLocaleTimeString();
  timeStrRef.value = newTimeStr;
}

setInterval(changeTime, 1000);


// const radiusInt = Math.round(Math.random() * 10);
// const PI = ref(3.14);
// const radius = ref(radiusInt);
// ref()とreactive()の違い
const data = reactive({
  PI: 3.14,
  radius: Math.round(Math.random() * 10),
})
const area = computed((): number => {
  return data.radius * data.radius * data.PI;
});

setInterval(
  ():void => {
    data.radius = Math.round(Math.random() * 10);
  },
  5000
);
console.log(data)
</script>

<template>
  <h1>こんにちは！{{ name }}さん</h1><br>

  <p>現在時刻：{{ timeStr }}</p><br>

  <p>現在時刻(ref)：{{ timeStrRef }}</p><br>

  <p>半径{{ data.radius }}の円の半径を円周率{{ data.PI }}で計算すると、{{ area }}</p>
</template>

