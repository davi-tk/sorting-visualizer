<template>
    <n-grid :cols="length" x-gap="10" :style="{AlignItems : 'end'}">
        <NGi v-for="value in array" >
            <Bar :size="value"/>
        </NGi>
    </n-grid>
</template>

<script setup lang="ts">
import { random } from 'lodash';
import Bar from './Bar.vue';
import {NGrid, NGi} from "naive-ui"

const props = defineProps<{
    length: number
}>()

const randomArray = (length : number, max : number) : number[] => [...new Array(length)]
    .map(() => random(1, max))

const array : number[] = randomArray(props.length, props.length )

</script>

<style scoped>

</style>