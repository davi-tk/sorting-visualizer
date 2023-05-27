<template>
    <NSelect v-model:value="value" :options="options" size="large" class="col-span-2"
    @update:value="emit('algorithm', algos[value])">

    </NSelect>
</template>

<script setup lang="ts">
import { NSelect } from 'naive-ui';
import { Ref, ref } from 'vue';

const value : Ref<number> = ref(-1)

const swap = (arr : number[], n:number, m:number) : void => {
    const aux  = arr[n]
    arr[n] = arr[m]
    arr[m]  = aux

} 

const bubbleSort = (arr : number[]) : void => {

    for (let i : number = 0; i < arr.length - 2; i++){
       if (arr[i] > arr[i + 1])
            swap(arr, i, i+1)
    }
}

const options = [

    {
        label : 'Select an algorithm',
        value : -1
    },
    {
        label : 'Bubble Sort',
        value : 0
    }
]

const algos : Function[] = [
    bubbleSort,
]

const emit = defineEmits<{
    (e : 'algorithm', value : Function ) : void
}>()

</script>

<style scoped>

</style>