<script setup lang="ts">
import { ref, computed } from 'vue'

const number = ref(80);
const showOrNot = computed(
  (): boolean => {
    let showOrNot = false;
    const rand = Math.round(Math.random() * 100);
    if(rand >= 50) {
      showOrNot = true;
    }
    return showOrNot;
  }
);

const randomNumber = computed(
  (): number => {
    return Math.round(Math.random() * 100);
  }
);

const cooktailListInit: string[] = ["ホワイトレディ", "ブルーハワイ", "ニューヨーク"];
const cooktailList = ref(cooktailListInit);

const changeCooktailList = (): void => {
  cooktailList.value = ["バラライカ", "XYZ", "マンハッタン"];
}
const addCooktailList = (): void => {
  cooktailList.value.push("ああああ");
}
const deleteFromCooktailList = (): void => {
  cooktailList.value.pop();
}

const cooktailListInit2: {[key: number]: string} = {
  2345: "ホワイトレディ", 
  4412: "ブルーハワイ", 
  6792: "ニューヨーク",
};
const cooktailList2 = ref(cooktailListInit2);

const cooktailListInitMap = new Map<number, string>();
cooktailListInitMap.set(5555, "ああああ");
cooktailListInitMap.set(5554, "いいい");
cooktailListInitMap.set(55333, "ううう");
cooktailListInitMap.set(55333, "ええええ");
const cooktailListMap = ref(cooktailListInitMap);

const changecooktailMap = (): void => {
  cooktailListMap.value.clear();
  cooktailListInitMap.set(5555, "ええええ");
  cooktailListInitMap.set(5554, "おおお");
  cooktailListInitMap.set(55333, "かかか");
}
const addCooktailMap = (): void =>{
  cooktailListMap.value.set(55555, "聞き聞き");
}
const deleteCooktailMap = (): void => {
  cooktailListMap.value.delete(5554);
}

const whiteLadyInit: {
  id: number;
  name: string;
  price: number;
  recipe: string;
} = {
  id: 2345,
  name: "ホワイトレディ",
  price: 1200,
  recipe: "ジン30ml+コワントロー15ml+レモン果汁15ml"
}
const whiteLady = ref(whiteLadyInit);
const changeWhiteLady = (): void => {
  whiteLady.value.price = 800;
}

const cooktailListArrayObjInit: Cooktail[] = [
  {id: 2345, name: "ホワイトレディ", price: 1200},
  {id: 4444, name: "ブルーハワイ", price: 1500},
  {id: 5466, name: "ニューヨーク", price: 1600},
  {id: 9022, name: "マティーニ", price: 1500},
];
const cooktailListArrayObj = ref(cooktailListArrayObjInit);

const cooktailListMapInit = new Map<number, Cooktail>();
cooktailListMapInit.set(2345, {id: 333, name: "あああ", price: 440});
cooktailListMapInit.set(23455, {id: 399, name: "いいい", price: 4490});
cooktailListMapInit.set(23444, {id: 3333, name: "ううう", price: 1500});
const cooktailListMap2 = ref(cooktailListMapInit);

const cooktail1500alfa = computed(
  (): Map<number, Cooktail> => {
    const newList = new Map<number, Cooktail>();
    cooktailListMap2.value.forEach(
      (value: Cooktail, key: number): void => {
        if(value.price == 1500) {
          newList.set(key, value);
        }
      }
    );
    return newList;
  }
);
const changeWhiteLadyPrice = (): void => {
  const whiteLady = cooktailListMap2.value.get(2345) as Cooktail;
  whiteLady.price = 1500;
}

interface Cooktail {
  id: number;
  name: string;
  price: number;
}

const cooktailDataList = ref(cooktailListArrayObjInit);
const cooktail1500 = computed(
  (): Cooktail[] => {
    const newList = cooktailDataList.value.filter(
      (cooktailItem: Cooktail): boolean => {
        return cooktailItem.price == 1500;
      }
    );
    return newList;
  }
)

</script>

<template>
  <section>
    <ul>
      <li v-for="[id, cooktailName] in cooktailListMap"
        v-binde:key="cooktailName">
        {{ cooktailName }}(インデックス{{ id }})
      </li>
    </ul>
    Cooktailを<button v-on:click="changecooktailMap">変更</button>
    Cooktailにブルームーンを<button v-on:click="addCooktailMap">追加</button>
    Cooktailからidが5554のものを<button v-on:click="deleteCooktailMap">削除</button>
  </section>
  <section>
    <ul>
      <li v-for="(cooktailName, index) in cooktailList"
        v-binde:key="cooktailName">
        {{ cooktailName }}(インデックス{{ index }})
      </li>
    </ul>
    Cooktailを<button v-on:click="changeCooktailList">変更</button>
    Cooktailにブルームーンを<button v-on:click="addCooktailList">追加</button>
    Cooktailから末尾のようを<button v-on:click="deleteFromCooktailList">削除</button>
  </section>
  <section>
    値段が1500のカクテルリスト
    <ul>
      <li v-for="cooktailItem in cooktail1500"
        v-bind:key="'cooktail1500' + cooktailItem.id">
        {{ cooktailItem.name }}の値段は{{ cooktailItem.price }}

      </li>
    </ul>
    <ul>
      <li v-for="[id, cooktailItem] in cooktail1500alfa"
      v-bind:key="id">
      {{ cooktailItem.name }}の値段は{{ cooktailItem.price }}円です。
      </li>
    </ul>
    あああの値段を1500円に<button v-on:click="changeWhiteLadyPrice">変更</button>
  </section>
  <section>
    <ul>
      <li v-for="r in 5"
        v-bind:key="r">
        半径{{ r }}の円の円周:{{ 2 * r * 3.14 }}
      </li>
    </ul>
  </section>
  Mapとオブジェクト配列の組み合わせ
  <section>
    <ul>
      <li v-for="[id, cooktailItem] in cooktailListMap2"
      v-bind:key="id">
      {{ cooktailItem.name }}の値段は{{ cooktailItem.price }}円です。
      </li>
    </ul>
  </section>
  オブジェクト配列のループ
  <section>
    <ul>
      <li
      v-for="cooktailItem in cooktailListArrayObj"
      v-bind:key="cooktailItem.id">
      {{ cooktailItem.name }}の値段は{{ cooktailItem.price }}円
      </li>
    </ul>
  </section>
  オブジェクトのループ
  <section>
    <dl>
      <template
      v-for="(value, key) in whiteLady"
      v-bind:key="key">
      <dt>{{ key }}</dt>
      <dd>{{ value }}</dd>
      </template>
    </dl>
    価格を1500円に<button v-on:click="changeWhiteLady">変更</button>
  </section>
  <section>
    <p v-if="number >= 50">1.条件に合致したため表示</p>
    <p v-if="Math.round(Math.random() * 100) >= 50">2.条件に合致したため表示</p>
    <p v-if="showOrNot">3.条件に合致したため表示</p>
    点数は{{ randomNumber }}で、
    <span v-if="randomNumber >= 80">優です。</span>
    <span v-else-if="randomNumber >= 70">良です。</span>
    <span v-else-if="randomNumber >= 60">可です。</span>
    <span v-else>不可です。</span>
    <p>
      点数は{{ randomNumber }}
      <template v-if="randomNumber >=80">
        で優です。
        <span style="color: red;">素晴らしい！！</span>
      </template>
    </p>
  </section>
  <section>
    <!-- v-showは常にレンダリングされてCSSの「display: none;」で表示・非表示を切り替えている
    頻繁に切り替わるような時はv-showが適している
    templateタグでは使えない！！ -->
    <p v-show="showOrNot">条件に合致したため表示</p>
  </section>
  <section>
    <ul>
      <li
        v-for="cooktailName in cooktailList"
        v-bind:key="cooktailName">
        {{ cooktailName }}
      </li>
    </ul>
    <ul>
      <li
        v-for="(cooktailName, index) in cooktailList"
        v-bind:key="cooktailName">
        {{ cooktailName }}(インデックス{{ index }})
      </li>
    </ul>
    <ul>
      <li
        v-for="(cooktailName, id) in cooktailList2"
        v-bind:key="'cooktailList' + id">
        {{ cooktailName }}(ID{{ id }})
      </li>
    </ul>
    <ul>
      <li
        v-for="(cooktailName, id, index) in cooktailList2"
        v-bind:key="'cooktailListWithId' + id">
        {{ index + 1 }}: IDが{{ id }}のカクテルは{{ cooktailName }}
      </li>
    </ul>
  </section>
  <!-- Mapのループ -->
  <section>
    <ul>
      <li
      v-for="[id, cooktailName] in cooktailListMap"
      v-bind:key="id">  
      IDが{{ id }}のカクテルは{{ cooktailName }}
      </li>
    </ul>
  </section>
</template>

<style>
  
</style>
