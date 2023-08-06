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
  <p v-bind:class="computedStyles">{{ msg2 }}</p><br>
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
