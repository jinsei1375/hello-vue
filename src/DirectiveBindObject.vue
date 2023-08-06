<script setup lang="ts">
import { ref, computed } from 'vue'


// style属性へのバインディング
const msg = ref("こんにちは世界");
const msgTextRed = ref("red");
const msgTextColor = ref("white");
const msgBgColor = ref("black");

const msgStyles = ref({
  color: "white",
  backgroundColor: "black"
});
const msgStyles2 = ref({
  fontSize: "24pt"
});
const msgStyles3 = ref({
  color: "pink",
  fontSize: "24pt"
});
const textSize =  computed(
  (): string => {
    const size = Math.round(Math.random() * 25) + 10;
    return `${size}pt`;
  }
);

// class属性へのバインディング
const msg2 = ref("こんにちは世界2");
const isTextColorRed = ref(true);
const isBgColorBlue = ref(false);
const styles = ref({
  textColorRed: false,
  bgColorBlue: true,
});
const computedStyles = computed(
  (): {textColorRed: boolean, bgColorBlue: boolean;} => {
    const randText = Math.round(Math.random());
    let textColorFlg = true;
    if(randText == 0) {
      textColorFlg = false;
    }
    const randBg = Math.round(Math.random());
    let bgColorFlg = true;
    if(randBg == 0) {
      bgColorFlg = false;
    }

    return {
      textColorRed: textColorFlg,
      bgColorBlue: bgColorFlg
    }
  } 
  )


  // イベントのディレクティブ
  const randValue = ref("まだです");
  const onButtonClick = (): void => {
    const rand = Math.round(Math.random() * 10);
    randValue.value = String(rand);
  }

  const mousePointerX = ref(0);
  const mousePointerY = ref(0);
  const onImgMousemove = (event: MouseEvent): void => {
    mousePointerX.value = event.offsetX;
    mousePointerY.value = event.offsetY;
  }

  const pBgColor = ref("white");
  const onPClick = (bgColor: string): void => {
    pBgColor.value = bgColor
  }

  const pMsg = ref("イベント前（ここをクリック！）");
  const pBgColorEvent = ref("white");
  const onClickWithEvent = (bgColor: string, event: MouseEvent): void => {
    pBgColorEvent.value = bgColor;
    pMsg.value = event.timeStamp.toString();
  }

  const errorMsg = ref("未送信");
  const onFormSubmit = (): void => {
    errorMsg.value = "送信されました。";
  }

  const clickMsg = ref("まだです！");
  const onEnterKey = (): void => {
    clickMsg.value = "エンターキーが押下されました。";
  }
  const onRightButtonKey = (): void => {
    clickMsg.value = "ボタンが右クリックされました。";
  }
  const onShiftClick = (): void => {
    clickMsg.value = "シフトを押しながらクリックされました。";
  }

</script>

<template>
  <p v-bind:style="{color: msgTextRed}">{{ msg }}</p><br>
  <p v-bind:style="{color: 'pink'}">{{ msg }}</p><br>
  <p v-bind:style="{fontSize: textSize}">{{ msg }}</p><br>
  <p v-bind:style="{color: msgTextColor, backgroundColor: msgBgColor}">{{ msg }}</p><br>
  <p v-bind:style="{color: msgTextColor, 'background-color': msgBgColor}">{{ msg }}</p><br>
  <p v-bind:style="msgStyles">{{ msg }}</p><br>
  <p v-bind:style="[msgStyles, msgStyles2]">{{ msg }}</p><br>
  <p v-bind:style="[msgStyles, msgStyles3]">{{ msg }}</p><br>
  <p v-bind:style="[msgStyles3, msgStyles]">{{ msg }}</p><br><br>

  <p v-bind:class="{textColorRed: true, bgColorBlue: true}">{{ msg2 }}</p><br>
  <p v-bind:class="{textColorRed: isTextColorRed, bgColorBlue: isBgColorBlue}">{{ msg2 }}</p><br>
  <p v-bind:class="{textColorPink: true}">{{ msg2 }}</p><br>
  <p v-bind:class="{'text-color-pink': true}">{{ msg2 }}</p><br>
  <p class="textSize24" v-bind:class="{textColorRed: isTextColorRed, bgColorBlue: isBgColorBlue}">{{ msg2 }}</p><br>
  <p class="textSize24" v-bind:class="styles">{{ msg2 }}</p><br>
  <p v-bind:class="computedStyles">{{ msg2 }}</p><br><br>

  <section>
    <button v-on:click="onButtonClick">クリック</button>
    <p>クリックの結果：{{ randValue }}</p>
    <img src="./assets/logo.svg" alt="" width="200" v-on:mousemove="onImgMousemove">
    <p>
      ポインタの位置： x={{ mousePointerX }}; y={{ mousePointerY }}
    </p>
    <p v-on:click="onPClick('red')" v-bind:style="{backgroundColor: pBgColor, color: 'black', cursor: 'pointer'}">ここをクリックすると背景色が変わります。</p><br>
    <p v-on:click="onClickWithEvent('green', $event)" v-bind:style="{backgroundColor: pBgColorEvent, color: 'black', cursor: 'pointer'}">{{ pMsg }}</p>

    <form action="#" v-on:submit.prevent="onFormSubmit">
      <input type="text" required><br>
      <button type="submit">送信</button>
      <p>{{ errorMsg }}</p><br>
      <p>{{ clickMsg }}</p>
    </form>
    <input type="text" v-on:keydown.enter="onEnterKey"><br>
    <input type="text" v-on:keydown.enter.exact="onEnterKey"><br><!-- Enterキーだけに制御 -->
    <button v-on:click.right="onRightButtonKey">右クリック</button>
    <button v-on:click.shift="onShiftClick">シフトを押しながらクリック</button>
  </section>


</template>

<style>
  .textColorRed {
    color: red;
  }
  .text-color-pink {
    color: pink;
  }
  .bgColorBlue {
    background-color: blue;
  }
  .textSize24 {
    font-size: 24px;
  }
</style>
