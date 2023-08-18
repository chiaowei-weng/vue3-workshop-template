<template>
  <div>
    <input type="text" @input="count = $event.target.value.length ?? 0">
    <span>
      <small>{{ count }} / {{ options.maxLength }}</small>
    </span>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  options: {
    type: Object,
    default: () => ({}),
  },
});

const count = ref(0);
</script>

<style scoped>
  span {
    margin-left: 10px;
  }
</style>