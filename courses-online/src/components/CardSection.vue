<template>
    <RoundedCard>
        <!--slots conditional-->

        <div v-if="$slots.header" class="p-4 text-medium border-b border-gray-200">
            <slot name="header">

            </slot>
        </div>
        <!--css conditional-->
        <div :class="{ 'p-4 text-medium border-b-20 border-gray-200': $slots.footer }">
            <slot></slot>

        </div>

        <!--slots conditional-->
        <div v-if="$slots.footer" class="p-4">

            <slot name="footer"></slot>


        </div>

    </RoundedCard>
</template>
<script setup>
import RoundedCard from "@/components/RoundedCard.vue";
</script>