<template>
    <section class="w-fit m-auto" id="#array" :style="{marginTop: '10%'}">
        <div class="place-items-end max-w flex gap-1"> 
            
            <div v-for="(value, index) in props.array" :key="index" ref="bar" 
            class="bg-neutral-300" :class="{'bg-red-400' : index == n || index == m}"
            :style="{height: `${((value/4) - length/20)/1.5 + 4}rem`, width: `calc(2rem - ${length/90}rem)`,
            minWidth: '5px'}">
            </div>
        </div>
    </section>

</template>

<script setup lang="ts">


const props = defineProps<{
    array : number[],
    length : number,
    n : number,
    m : number
}>()



</script>

<style scoped></style>