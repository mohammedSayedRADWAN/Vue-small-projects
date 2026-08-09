<script setup>
import { ref } from "vue";
const counter = ref(0);


const decrement = () => {
  counter.value--;
};
</script>

<template>
  <h1>Counter is {{ counter }}</h1>
  <button @click="counter++">Increment +1</button>
  <button @click="decrement">Decrement -1</button>
</template>

<style scoped></style>
