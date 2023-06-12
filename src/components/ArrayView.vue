<template>
    <section class="w-fit m-auto" id="#array" :style="{marginTop: '10%'}">
        <div class="place-items-end max-w flex" style="gap: 1px;"> 
            
            <div v-for="(value, index) in props.array" :key="index"
            class="text-center text-neutral-800 font-bold" :class="{'bg-blue-400 animate-bounce' : (index == props.n || index == props.m)
            , 'bg-emerald-400' : positioned.includes(index), 'bg-neutral-300' : (index !== props.n && index !== props.m && !positioned.includes(index))}"
            :style="{height: `${(value/10) + 0.5}rem`, width: `${2 - (length/100)}rem`,
            minWidth: '5px'}">
            <p v-show="length <= 50">{{ value }}</p>
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
    positioned : number[]
}>()





</script>

<style scoped></style>