<script setup>

const props = defineProps({
  prepend: {
    type: String,
    default: "",
  },
  append: {
    type: String,
    default: "",
  },
});

</script>

<template>
  <div class="input-slot">
    <div class="prepend" v-if="$slots.prepend">
      <slot name="prepend">
        <div v-if="prepend"> {{ prepend }}</div>
      </slot>
    </div>
    <input type="text" :class="{'has-append': $slots.append , 'has-prepend': $slots.prepend}"/>
    <div class="append" v-if="$slots.append">
      <slot name="append" >
        <div v-if="append"> {{ append }}</div>
      </slot>
    </div>
  </div> 
</template>

<style scoped>
* {
  box-sizing: border-box;
}
.input-slot {
  display: flex;
}

input {
  border: 1px solid lightskyblue;
  border-radius: 4px;
  &:focus,&:active {
   outline: none;
  }
  &.has-prepend {
    border-radius: 0 4px  4px 0;
  }
  &.has-append {
    border-radius:  4px 0 0 4px ;
  }
  &.has-prepend.has-append {
    border-radius:  0 ;
  }
}
.prepend, .append {
  width: fit-content;
  padding: 0 8px;
  min-height: 30px;
  border: 1px solid lightskyblue;
  background: lightcyan;
  display: flex;
  align-items: center;
  color:cornflowerblue;
}
.prepend {
  border-radius: 4px 0 0 4px ;
  border-right: none;
}
.append {
  border-radius:  0 4px 4px 0;
  border-left: none;
}
</style>