<template>
    <RoundedCard>
        <div class="p-4 text-medium border-b border-gray-200">
            <slot name="header">

            </slot>
        </div>
        <div class="p-4 text-medium border-b border-gray-200">
            <slot></slot>

        </div>


        <div class="p-4">

            <slot name="footer"></slot>


        </div>

    </RoundedCard>
</template>
<script setup>
import RoundedCard from "@/components/RoundedCard.vue";
</script>