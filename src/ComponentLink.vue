<script setup lang="ts">
import { ref, computed } from 'vue';
import OneSection from './components/OneSection.vue';
import WithModel from './components/WithModel.vue';
import OneInfo from './components/OneInfo.vue';
import OneMember from './components/OneMember.vue';
import OneMemberModel from './components/OneMemberModel.vue';

const memberListInit = new Map<number, Member>();
memberListInit.set(33456, {id: 33456, name: "田中太郎", email: "aaa@aaa.com", points: 100, note: "初回特典あり"});
memberListInit.set(4778, {id: 4778, name: "鈴木じろう", email: "bbb@bbb.com", points: 10});
const memberList = ref(memberListInit);

const totalPoints = computed(
  (): number => {
    let total = 0;
    for(const member of memberList.value.values()) {
      total += member.points;
    }
    return total;
  }
)

// Emitにより実行されるメソッド
const onIncrementPoint = (id: number): void => {
  const member = memberList.value.get(id);
  if(member != undefined) {
    member.points++;
  }
}

const rand = Math.round(Math.random() * 10);
const propsNumber = ref(rand);

const weatherListInit = new Map<number, Weather>();
weatherListInit.set(1, {id: 1, title: "今日の天気", content: "今日は晴れでしょう。"});
weatherListInit.set(2, {id: 2, title: "明日の天気", content: "今日は雨でしょう。"});
weatherListInit.set(3, {id: 3, title: "明後日の天気", content: "今日は曇りでしょう。"});
const weatherList = ref(weatherListInit);

interface Weather {
  id: number;
  title: string;
  content: string;
}
interface Member {
  id: number;
  name: string;
  email: string;
  points: number;
  note?: string;
}

</script>

<template>
  <h1>コンポーネント基礎</h1>
  <section>
    <h2>コンポーネント1個</h2>
    <OneSection />
  </section>
  <section>
    <h2>コンポーネントが複数</h2>
    <OneSection />
    <OneSection />
    <OneSection />
  </section>

  <h1>コンポーネントの独立性</h1>
  <section>
    <h2>v-modelを含むコンポーネント</h2>
    <WithModel />
    <WithModel />
  </section>

  <h1>Props基礎</h1>
  <!-- テンプレート変数を用いる場合はv-bindディレクティブを使う -->
  <section>
    <h2>属性に直接記述</h2>
    <OneInfo
      title="Propsの利用"
      content="子コンポーネントにデータを渡すにはPropsを利用する"
      v-bind:number="propsNumber"
    />
  </section>

  <section>
    <h2>ループでコンポーネントを生成</h2>
    <OneInfo
      v-for="[id, weather] in weatherList"
      v-bind:key="id"
      v-bind:title="weather.title"
      v-bind:content="weather.content"
      v-bind:number="propsNumber"
    />
  </section>

  <section>
    <h1>会員リスト</h1>
    <p>会員全員の保有ポイント：{{ totalPoints }}</p>
    <OneMember
      v-for="[id, member] in memberList"
      v-bind:key="id"
      v-bind:id="id"
      v-bind:name="member.name"
      v-bind:email="member.email"
      v-bind:points="member.points"
      v-bind:note="member.note"
      v-on:incrementPoint="onIncrementPoint"
    />
  </section>
  <section>
    <h1>会員リスト</h1>
    <p>全会員の保有ポイント：{{ totalPoints }}</p>
    <OneMemberModel
      v-for="[id, member] in memberList"
      v-bind:key="id"
      v-bind:id="id"
      v-bind:name="member.name"
      v-bind:email="member.email"
      v-model:points="member.points"
      v-bind:note="member.note" />
  </section>

</template>

<style>
  section {
    border: 1px solid blue;
    margin: 10px;
  }
</style>
