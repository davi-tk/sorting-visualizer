<template>
    <section class="w-fit m-auto" id="#array">
        <div class="place-items-end max-w flex gap-1"> 
            
            <div v-for="(value, index) in props.array" :key="index" 
            class="bg-neutral-300 "
            :style="{height: `calc(${(value/4 + 2)}rem - ${length/100}rem)`, width: `calc(1.5rem - ${length/100}rem)`}">
            </div>
        </div>
    </section>

</template>

<script setup lang="ts">

const props = defineProps<{
    array : number[],
    length : number
}>()

const sortArray = (array : number[]) : number[] => array.sort((a, b) => a - b)

</script>

<style scoped></style>