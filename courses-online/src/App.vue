<template>

  <div class="p-4 space-y-8">
    <h1 class="text-4xl font-medium">cources hub</h1>
    <h2 class="text-2xl font-medium">all courcess</h2>
    <div v-if="flag" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <SkelatonCourses v-for="i in 4"></SkelatonCourses>

    </div>
    <div v-if="flag" class="text-2xl font-medium">courcess are loading...</div>
    <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <course-items v-for="course in courses" :key="course.id" :title="course.title" :price="course.price"
        :description="course.description" @click="console.log('button clicked')"></course-items>

    </div>
    <h2 class="text-2xl font-medium">your cources</h2>
    <div class="grid grid-cols-1 gap-4">
      <BookingItem v-for="i in 2" :key="i" />
    </div>
  </div>

</template>
<script setup>
import { ref, onMounted } from "vue";
import CourseItems from "@/components/CourseItems.vue";
import BookingItem from "@/components/boockingItem.vue";
import SkelatonCourses from "@/components/SkelatonCourses.vue";


const courses = ref([])
const flag = ref(false)
const fetchCources = async () => {
  flag.value = true

  try {
    const res = await fetch("http://localhost:5000/courses")
    courses.value = await res.json()

  } catch (e) {
    console.log(e)
  } finally {
    flag.value = false
  }
}

onMounted(() => {
  fetchCources()
})
</script>