<script setup lang="ts">
import { ref } from 'vue'

const inputNameModel = ref("双方向");

const inputNameBind = ref("しんちゃん");
const inputNameOn = ref("ななし");
const onInputName = (event: Event): void => {
  const element = event.target as HTMLInputElement;
  inputNameOn.value = element.value;
}

const inputTextArea = ref("テキストエリアへの入力文字、\n改行も入れてみる");
const memberType = ref(1);
const memberTypeSelect = ref(1);
const isAgreed = ref(false);
const isAgreed01 = ref(0);
const selectedOS = ref([]);
const selectedOSSelect = ref([]);

const htmlStr = ref(`<a href="https://google.com">googleトップページ</a>`);

const price = ref(1000);

const hello = ref("こんにちは");

</script>

<template>
  <section>
    <input type="text" name="" id="" v-model="inputNameModel">
    <p>{{ inputNameModel }}</p><br>

    <input type="text" v-bind:value="inputNameBind"><br>
    <input type="text" v-on:input="onInputName"><br>
    <p>{{ inputNameOn }}</p>
  </section>

  <section>
    <textarea v-model="inputTextArea" name="" id="" cols="30" rows="10"></textarea><br>
    <label for=""><input type="radio" name="memberType" value="1" v-model="memberType">通常会員</label>
    <label for=""><input type="radio" name="memberType" value="2" v-model="memberType">特別会員</label>
    <label for=""><input type="radio" name="memberType" value="3" v-model="memberType">有料会員</label><br>
    <p>選択されたラジオボタン:{{ memberType }}</p><br>

    <select name="" id="" v-model="memberTypeSelect">
      <option value="1">通常会員</option>
      <option value="2">特別会員</option>
      <option value="3">有料会員</option>
    </select><br>
    <p>選択されたリスト:{{ memberTypeSelect }}</p><br>

    <label for=""><input type="checkbox" v-model="isAgreed">同意する</label><br>
    <p>同意の結果：{{ isAgreed }}</p><br>
    <label for=""><input type="checkbox" v-model="isAgreed01" true-value="1" false-value="0">同意する</label><br>
    <p>同意の結果：{{ isAgreed01 }}</p><br>

    <label for=""><input type="checkbox" v-model="selectedOS" value="1">macOS</label>
    <label for=""><input type="checkbox" v-model="selectedOS" value="2">Windows</label>
    <label for=""><input type="checkbox" v-model="selectedOS" value="3">Linux</label>
    <label for=""><input type="checkbox" v-model="selectedOS" value="4">iOS</label>
    <label for=""><input type="checkbox" v-model="selectedOS" value="5">Android</label><br>
    <p>選択されたOS:{{ selectedOS }}</p><br>

    <select name="" id="" v-model="selectedOSSelect" multiple>
      <option value="1">macOS</option>
      <option value="2">Windows</option>
      <option value="3">Linux</option>
      <option value="4">iOS</option>
      <option value="5">Android</option>
    </select>
    <p>選択されたOS:{{ selectedOSSelect }}</p><br>

    <section>
      {{ htmlStr }}
      <section v-html="htmlStr"></section>
    </section>

    <section v-pre>
      <p v-html="htmlStr">{{ htmlStr }}</p>
    </section>

    <section>
      <input type="number" v-model="price">円<br>
      <p>金額は{{ price }}円です。</p>
      <p v-once>金額は{{ price }}円です。</p>
    </section>

    <p v-cloak>{{ hello }}</p>

  </section>


</template>

<style>
  [v-cloak] {
    display: none;
  }
</style>
