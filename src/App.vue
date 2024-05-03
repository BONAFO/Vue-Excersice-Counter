<!-- Contador que aumente y disminuya por buttons -->
<!-- Button para resetear -->
<!-- Red < 0 , Yellow = 0 , Green > 0 -->

<template>
  <div>
    <h3 class="counter">
      Counter: <span :class="`c-c-${counter_color}`">{{ counter }}</span>
    </h3>
    <br />
    <div>
      <button @click="update_counter('d')"  class="btn btn-r">-</button>
      <button @click="update_counter('r')"  class="btn btn-y">Reset</button>
      <button @click="update_counter('a')"  class="btn btn-g">+</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const change_color = () => {

  if (counter.value < 0) {
    return "r";
  } else if (counter.value > 0) {
    return "g";
  } else {
    return "y";
  }
};

const update_counter = (op) => {
  if (op == "a") {
    counter.value++;
  } else if (op == "d") {
    counter.value--;
  } else {
    counter.value = 0;
  }
  counter_color.value = change_color();
};

const counter = ref(0);
const counter_color = ref("y");


</script>

<style scoped>
@import url("style/style.css");
</style>
