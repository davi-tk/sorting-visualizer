<template>
    <section class="w-fit m-auto" id="#array" :style="{marginTop: '10%'}">
        <div class="place-items-end max-w flex gap-1"> 
            
            <div v-for="(value, index) in props.array" :key="index" 
            class="bg-neutral-300 "
            :style="{height: `${((value/4) - length/20)/1.5}rem`, width: `calc(1.5rem - ${length/100}rem)`}">
            </div>
        </div>
    </section>

</template>

<script setup lang="ts">

const props = defineProps<{
    array : number[],
    length : number
}>()


</script>

<style scoped></style>