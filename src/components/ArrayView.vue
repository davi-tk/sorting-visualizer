<template>
    <section class="w-fit m-auto" id="#array" :style="{marginTop: '10%'}">
        <div class="place-items-end max-w flex gap-1"> 
            
            <div v-for="(value, index) in props.array" :key="index"
            class="text-center text-neutral-800 font-bold" :class="{'bg-blue-400 animate-bounce' : (index == props.n || index == props.m)
            , 'bg-emerald-400' : done || positioned.includes(index), 'bg-neutral-300' : (!done && index !== props.n && index !== props.m && !positioned.includes(index))}"
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
    done : boolean,
    positioned : number[]
}>()



</script>

<style scoped></style>