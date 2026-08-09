<script setup>
const counter = 0;

</script>

<template>
  <h1>Counter is {{ counter }}</h1>
  <button @click="increment">Increment +1</button>
  <button @click="decrement">Decrement -1</button>
</template>

<style scoped></style>
