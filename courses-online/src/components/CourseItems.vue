<template>
    <div class="bg-white border border-gray-200 rounded-md">
        <h3 class="p-4 text-medium border-b border-gray-200">{{ title }}</h3>
        <p class="p-4 text-medium border-b border-gray-200">{{ price }}</p>
        <p class="p-4 text-medium">{{ description }}</p>
    </div>
</template>
<script setup> defineProps({
    title: String,           
    price: Number,
    description: String,
}
    
)</script>