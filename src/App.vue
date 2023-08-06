<script setup lang="ts">
import { ref, computed, reactive } from 'vue'

const name = ref("田中太郎");

// 時刻表示
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

// 計算結果表示

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

// ディレクティブ
const url = ref("https://vuejs.org/");
const isSendButtonDisabled = ref(true);
const widthOrHeight = ref("height");
const widthOrHeightValue = ref(100);
const imgAttributes = ref({
  src: "images/logo.svg",
  alt: "Vueのロゴ",
  width: 75,
  height: 75,
});

const msg = "";

</script>

<template>
  <h1>こんにちは！{{ name }}さん</h1><br>

  <p>現在時刻：{{ timeStr }}</p><br>

  <p>現在時刻(ref)：{{ timeStrRef }}</p><br>

  <p>半径{{ data.radius }}の円の半径を円周率{{ data.PI }}で計算すると、{{ area }}</p><br>

  <p><a v-bind:href="url" target="_blank">Vue.jsのサイト</a></p><br>
  <p><a :href="url" target="_blank">Vue.jsのサイト(省略形) </a></p><br>
  <p><a v-bind:href="url + 'guide/introduction.html'" target="_blank">Vue.jsガイドのページ </a></p><br>
  <p><button type="button" v-bind:disabled="isSendButtonDisabled">送信</button></p><br>
  <p>
    <img src="./assets/logo.svg" alt="" v-bind:[widthOrHeight]="widthOrHeightValue">
  </p><br>
  <p>
    <img v-bind="imgAttributes">
  </p><br>
  <p>
    <img v-bind="imgAttributes" title="ロゴです！">
  </p><br>
  <p>
    <img v-bind="imgAttributes" alt="ロゴです！">
  </p><br>
</template>

