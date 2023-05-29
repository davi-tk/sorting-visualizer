<template>
    <NSelect v-model:value="value" :options="options" size="large" class="col-span-2"
        @update:value="emit('algorithm', algos[value])">

    </NSelect>
</template>

<script setup lang="ts">
import { NSelect } from 'naive-ui';
import { Ref, ref } from 'vue';

const value: Ref<number> = ref(-1)

const swap = (arr: number[], n: number, m: number): void => {
    const aux = arr[n]
    arr[n] = arr[m]
    arr[m] = aux

}

function sleep(ms: number) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

const bubbleSort = async (arr: number[], n: Ref<number>, m: Ref<number>, active: Ref<boolean>, done: Ref<boolean>, delay: number, positioned: Ref<number[]>): Promise<void> => {

    active.value = false


    let checked: boolean;
    let j: number = 0
    do {
        checked = false;
        for (let i = 0; i < arr.length - j - 1; i++) {
            n.value = i
            m.value = i + 1
            console.log(j, i)

            if (arr[i] > arr[i + 1]) {
                swap(arr, i, i + 1)
                checked = true;
            }
            await sleep(delay)

        }
        positioned.value.push(arr.length - 1 - j)
        j++
    } while (checked && j < arr.length);

    n.value = -1
    m.value = -1
    active.value = true
    done.value = true
}

const selectionSort = async (arr: number[], n: Ref<number>, m: Ref<number>, active: Ref<boolean>, done: Ref<boolean>, delay: number, positioned: Ref<number[]>): Promise<void> => {

    active.value = false


    for (let i = 0; i < arr.length; i++) {
        let min = i;
        n.value = i
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[min]) {
                min = j;
            }
        }
        if (min != i) {
            m.value = min
            await (sleep(delay))
            swap(arr, min, i)
        }

        positioned.value.push(i)
    }

    n.value = -1
    m.value = -1
    active.value = true
    done.value = true
}

const options = [

    {
        label: 'Select an algorithm',
        value: -1,
        disabled: true
    },
    {
        label: 'Bubble Sort',
        value: 0
    },
    {
        label: 'Selection Sort',
        value: 1
    }
]

const algos: Function[] = [
    bubbleSort,
    selectionSort,
]

const emit = defineEmits<{
    (e: 'algorithm', value: Function): void
}>()

</script>

<style scoped></style>