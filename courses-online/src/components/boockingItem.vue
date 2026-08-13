<template>
    <CardSection>


        <div class="flex justify-between items-center">
            <div>
                vue course, 100 , learn from scratch and master the fundamentals
            </div>
            <RoundedButton @click="console.log('report')" variant="danger">Report</RoundedButton>
        </div>


    </CardSection>



</template>
<script setup>
import RoundedButton from "@/components/RoundedButton.vue";
import CardSection from "@/components/CardSection.vue";
</script>