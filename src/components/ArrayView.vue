<template>
    <section class="w-fit m-auto" id="#array" :style="{marginTop: '10%'}">
        <div class="place-items-end max-w flex gap-1"> 
            
            <div v-for="(value, index) in props.array" :key="index" ref="bar" 
            class="bg-neutral-300 text-center text-green-700 font-bold" :class="{'bg-blue-400 animate-bounce' : (index == props.n || index == props.m)
            , 'bg-blue-300' : done}"
            :style="{height: `${(value/6) +1.5}rem`, width: `calc(2rem - ${length/70}rem)`,
            minWidth: '5px'}">
            <p v-show="length <= 30">{{ value }}</p>
            </div>
        </div>
    </section>

</template>

<script setup lang="ts">


const props = defineProps<{
    array : number[],
    length : number,
    n : number,
    m : number,
    done : boolean
}>()



</script>

<style scoped></style>