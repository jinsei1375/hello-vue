<script setup lang="ts">
import { provide, reactive } from 'vue';
import BaseSection from './components/BaseSection.vue';
import type {Member} from './interfaces';

const memberList = new Map<number, Member>();
memberList.set(33456, {id: 33456, name: "田中太郎", email: "aaa@aaa.com", points: 100, note: "初回特典あり"});
memberList.set(4778, {id: 4778, name: "鈴木じろう", email: "bbb@bbb.com", points: 10});

provide("memberList", reactive(memberList));

</script>

<template>
  <BaseSection />
</template>

<style>
  section {
    border: 1px solid blue;
    margin: 10px;
  }
</style>
