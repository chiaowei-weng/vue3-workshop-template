<script setup>
import { computed, ref, watch } from "vue";

const inputValue = ref("");

const handleClick = () => {
    if (!inputValue.value) {
      return
    }
    //
    navigator.clipboard.writeText(inputValue.value)
    .then(() => {
      console.log('複製成功');
      alert("複製成功:" + inputValue.value);
    });
}

</script>

<template>
  <input v-model="inputValue" @click="handleClick"/>
</template>


<style>
.class{
  color: red;
}
</style>
