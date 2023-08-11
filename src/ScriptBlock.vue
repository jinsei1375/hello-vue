<script setup lang="ts">
import { ref, computed, watchEffect, watch } from 'vue'

const cooktailDataListInit = new Map<number, Cooktail>();
cooktailDataListInit.set(1, {id: 1, name: "ホワイトレディ", price: 1200});
cooktailDataListInit.set(2, {id: 2, name: "ブルーハワイ", price: 1500});
cooktailDataListInit.set(3, {id: 3, name: "ニューヨーク", price: 1100});
cooktailDataListInit.set(4, {id: 4, name: "マティーニ", price: 1500});
const cooktailNo = ref(1);
const priceMsg = computed(
  (): string => {
    const cooktail = cooktailDataListInit.get(cooktailNo.value);
    let msg = "該当カクテルはありません。";
    if(cooktail != undefined) {
      msg = `該当するカクテルは${cooktail.name}で価格は${cooktail.price}です。`;
    }
    return msg;
  }
);

const priceMsgWatch = ref("");
// watcheffct関数
// 引数としてコールバック関数を受け取る、中身の値が変わるのを監視する
// watchEffect(
//   (): void => {
//     priceMsgWatch.value = getCooktailInfo(cooktailNo.value);
//   }
// );

// watch()関数は初回起動時にはコールバック関数は実行されない！！
// 初回起動させるには第三引数に{immediate: true}を追加する
// watch(cooktailNo,
//   (): void => {
//     priceMsgWatch.value = getCooktailInfo(cooktailNo.value);
//   },
//   {immediate: true}
// );

// 変更前後の値の利用
watch(cooktailNo,
  (newVal: number, oldVal: number): void => {
    let msg = "前のカクテル: ";
    msg += getCooktailInfo(oldVal);
    msg += "現在のカクテル: ";
    msg += getCooktailInfo(newVal);
    priceMsgWatch.value = msg;
  }
)

function getCooktailInfo(cooktailNo: number): string {
  const cooktailDataListInit = new Map<number, Cooktail>();
  cooktailDataListInit.set(1, {id: 1, name: "ホワイトレディ", price: 1200});
  cooktailDataListInit.set(2, {id: 2, name: "ブルーハワイ", price: 1500});
  cooktailDataListInit.set(3, {id: 3, name: "ニューヨーク", price: 1100});
  cooktailDataListInit.set(4, {id: 4, name: "マティーニ", price: 1500});
  const cooktail = cooktailDataListInit.get(cooktailNo);
  let msg = "該当カクテルはありません。";
  if(cooktail != undefined) {
    msg = `該当するカクテルは${cooktail.name}で価格は${cooktail.price}です。`;
  }
  return msg;
}
setInterval(
  (): void => {
    cooktailNo.value = Math.round(Math.random() * 3) + 1;
  },
  1000
);

interface Cooktail {
  id: number;
  name: string;
  price: number;
}

</script>

<template>
  <section>
    <p>現在のカクテル番号：{{ cooktailNo }}</p>
    <p>{{ priceMsg }}</p>
    <p>{{ priceMsgWatch }}</p>
  </section>
</template>

<style>
  
</style>
