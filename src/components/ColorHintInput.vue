<template>
  <div>
    <input
      :style="{ color: textColor }"
      type="text"
      v-model="inputText"
    >
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";

const props = defineProps({
  options: {
    type: Object,
    default: () => ({}),
  },
});

// 整理資料
const { maxLength, colorSets } = props.options;
const boundaryVals = [];
const colors = []

colorSets.sort((a, b) => (b.charsLeftUnder - a.charsLeftUnder));

colorSets.forEach((colorSet) => {
  if (colorSet.charsLeftUnder === undefined || colorSet.color === undefined) {
    throw new Error("ColorHintInput 元件顏色組合資料設定不完整");
  }
  if (colorSet.charsLeftUnder < 0) {
    throw new Error("ColorHintInput 元件顏色組合 charsLeftUnder 不可為負值");
  }
  boundaryVals.push(colorSet.charsLeftUnder);
  colors.push(colorSet.color);
})

const setsNum = boundaryVals.length;

// 運作邏輯
const inputText = ref('');

watch(inputText, (nowText, preText) => {
  if (nowText.length > maxLength) {
    inputText.value = preText;
  }
})

const textColor = computed(() => {
  const charsLeft = maxLength - inputText.value.length;
  if (charsLeft > boundaryVals[0]) {
    return "";
  }
  if (charsLeft <= boundaryVals[setsNum - 1]) {
    return colors[setsNum - 1];
  }
  for (let i = 0; i < setsNum - 1; i += 1) {
    if (charsLeft <= boundaryVals[i] && charsLeft > boundaryVals[i + 1]) {
      return colors[i];
    }
  }
});
</script>
