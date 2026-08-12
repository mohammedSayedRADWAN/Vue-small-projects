<template>

<div class="p-4 space-y-8">
  <h1 class="text-4xl font-medium">cources hub</h1>
<h2 class="text-2xl font-medium">all courcess</h2>
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
  <course-items v-for="i in 3"></course-items>

</div> <h2 class="text-2xl font-medium">your cources</h2>
</div>

</template>
<script setup>
import CourseItems from "@/components/CourseItems.vue";
</script>
 