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

const customDone = async (arr: number[], positioned: Ref<number[]>): Promise<void> => {
    for (let i = 0; i < arr.length; i++) {

        if (i == arr.length - 1) {

            positioned.value.push(i)
            return
        }

        else if (i > i + 1) console.log('deu merda')

        await sleep(5)
        positioned.value.push(i)
    }



}

const bubbleSort = async (arr: number[], n: Ref<number>, m: Ref<number>, delay: number, positioned: Ref<number[]>): Promise<number[]> => {

    let checked: boolean;
    let j: number = 0
    do {
        checked = false;
        for (let i = 0; i < arr.length - j - 1; i++) {
            n.value = i
            m.value = i + 1


            if (arr[i] > arr[i + 1]) {
                swap(arr, i, i + 1)
                checked = true;
            }
            await sleep(delay)


        }
        j++
    } while (checked && j < arr.length);

    n.value = -1
    m.value = -1

    await customDone(arr, positioned)
    return arr

}

const selectionSort = async (arr: number[], n: Ref<number>, m: Ref<number>, delay: number, positioned: Ref<number[]>): Promise<number[]> => {

    for (let i = 0; i < arr.length; i++) {
        let min = i;
        n.value = i
        for (let j = i + 1; j < arr.length; j++) {
            await (sleep(delay))
            if (arr[j] < arr[min]) {
                min = j;
            }
        }
        if (min != i) {
            m.value = min
            swap(arr, min, i)
        }

    }

    n.value = -1
    m.value = -1

    await customDone(arr, positioned)
    return arr


}

const insertionSort = async (arr: number[], n: Ref<number>, m: Ref<number>, delay: number, positioned: Ref<number[]>): Promise<number[]> => {

    for (let i = 0; i < arr.length; i++) {
        let key = arr[i]
        let j = i - 1

        while (j >= 0 && key < arr[j]) {
            n.value = j
            m.value = j + 1
            arr[j + 1] = arr[j]
            j--
            await sleep(delay)
        }
        arr[j + 1] = key
    }

    n.value = -1
    m.value = -1

    await customDone(arr, positioned)
    return arr


}

const quickSort = async (arr: number[], n: Ref<number>, m: Ref<number>, delay: number, positioned: Ref<number[]>): Promise<number[]> => {

    const partition = async (arr: number[], low: number, high: number): Promise<number> => {
        let pivot = arr[high];

        let i = (low - 1);
        for (let j = low; j <= high - 1; j++) {
            n.value = i
            m.value = j
            await sleep(delay)
            if (arr[j] <= pivot) {
                i++;

                swap(arr, i, j)

            }
        }


        await sleep(delay)
        swap(arr, i + 1, high)

        return i + 1;
    }

    const sort = async (arr: number[], low: number, high: number): Promise<number[]> => {
        if (low < high) {

            let partitionIndex = await partition(arr, low, high);
            arr = await sort(arr, low, partitionIndex - 1);
            arr = await sort(arr, partitionIndex + 1, high);

        }
        return arr
    }

    await sort(arr, 0, arr.length - 1)

    n.value = -1
    m.value = -1
    await customDone(arr, positioned)

    return arr

}

const mergeSort = async (arr: number[], n: Ref<number>, m: Ref<number>, delay: number, positioned: Ref<number[]>): Promise<number[]> => {


    const merge = async (arr: number[], start: number, mid: number, end: number): Promise<void> => {
        let start2 = mid + 1;

        if (arr[mid] <= arr[start2]) {
            return;
        }


        while (start <= mid && start2 <= end) {

            n.value = start
            m.value = start2

            if (arr[start] <= arr[start2]) {

                start++;
            }
            else {
                let value = arr[start2];
                let index = start2;


                while (index != start) {
                    await sleep(delay)
                    
                    arr[index] = arr[index - 1];
                    index--;

                }
                arr[start] = value;

                start++;
                mid++;
                start2++;
            }
        }
    }


    const sort = async (arr: number[], l: number, r: number): Promise<number[]> => {
        if (l < r) {

            // Same as (l + r) / 2, but avoids overflow
            // for large l and r
            let m = l + Math.floor((r - l) / 2);

            // Sort first and second halves
            await sort(arr, l, m);
            await sort(arr, m + 1, r);

            await merge(arr, l, m, r);
        }

        return arr
    }

    await sort(arr, 0, arr.length - 1)
    n.value = -1
    m.value = -1
    await customDone(arr, positioned)
    return arr
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
    },
    {
        label: 'Insertion Sort',
        value: 2
    },
    {
        label: 'Quick Sort',
        value: 3
    },
    {
        label: 'Merge Sort',
        value: 4
    }
]

const algos: Function[] = [
    bubbleSort,
    selectionSort,
    insertionSort,
    quickSort,
    mergeSort,
]

const emit = defineEmits<{
    (e: 'algorithm', value: Function): void
}>()

</script>

<style scoped></style>