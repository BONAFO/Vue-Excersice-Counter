<!-- Contador que aumente y disminuya por buttons -->
<!-- Button para resetear -->
<!-- Red < 0 , Yellow = 0 , Green > 0 -->
<!-- Agregar button para favoritos -->
<!-- Bloquear el button para que no se pueda agregar el mismo -->
<!-- Mostar array como lista -->
<template>
  <div>
    <h3 class="counter">
      Counter: <span :class="`c-c-${counter_color}`">{{ counter }}</span>
    </h3>
    <br />
    <div>
      <button @click="update_counter('d')" class="btn btn-r">-</button>
      <button @click="update_counter('r')" class="btn btn-y">Reset</button>
      <button @click="update_counter('a')" class="btn btn-g">+</button>
      <button
        @click="add_favorite()"
        :class="`btn btn-f ${isFavorite ? 'disabled' : ''}`"
        :disabled="isFavorite"
      >
        Favorite
      </button>

      <button
        @click="delete_favorite()"
        :class="`btn btn-f ${!isFavorite ? 'disabled' : ''}`"
        :disabled="!isFavorite"
      >
        Delete
      </button>
    </div>

    <div class="fav-cont">
      <h3 class="fav-title">Your numbers:</h3>
      <ul class="fav-title">
        <li v-for="num in favorites" class="fav-item">{{ num }}</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";

const add_favorite = () => {
  favorites.value.push(counter.value)
};
const delete_favorite = () => {
  favorites.value = favorites.value.filter(f => f !== counter.value);
};

const update_counter = (op) => {
  if (op == "a") {
    counter.value++;
  } else if (op == "d") {
    counter.value--;
  } else {
    counter.value = 0;
  }
};

const favorites = ref([]);

const counter = ref(0);

const counter_color = computed(() => {
  if (counter.value < 0) {
    return "r";
  } else if (counter.value > 0) {
    return "g";
  } else {
    return "y";
  }
});

const isFavorite = computed(() => {
  if (favorites.value.indexOf(counter.value) !== -1) {
    return true;
  } else {
    return false;
  }
});
</script>

<style scoped>
@import url("style/style.css");
</style>
