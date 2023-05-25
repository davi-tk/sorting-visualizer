<script setup lang="ts">
import { ref, Ref, watch } from 'vue';
import { random } from 'lodash';
import { NSlider, NInputNumber, NButton } from 'naive-ui';
import ArrayView from './components/ArrayView.vue';

const min: number = 50
const length: Ref<number> = ref(min)

const randomArray = (length: number, min: number, max: number): number[] => [...new Array(length)].map(() => random(min / 2, max))

const array: Ref<number[]> = ref(randomArray(length.value, 50, length.value * 2))

watch(length, () => array.value = randomArray(length.value, 50, length.value * 2))

const sortArray = (array: number[]): number[] => array.sort((a, b) => a - b)

</script>

<template>
  <section id="controllers" class="grid grid-flow-col grid-cols-10 items-end">
    <div id="slider" class="pt-4 pl-4 col-span-2">
      <h3 class="text-lg">Array size</h3>
      <n-slider :min=min v-model:value="length" :step="2" class="my-4" />
      <n-input-number :min="min" v-model:value="length" size="large" />
    </div>
    <NButton @click="sortArray(array)" type="info" ghost size="large" class="mx-8">Sort!</NButton>
    <NButton @click="array = randomArray(length, 50, length * 2)" type="primary" ghost size="large" class="col-span-2 mx-8">Generate New Array</NButton>
  </section>

  <ArrayView :length="length" :array="array" />
</template>

<style scoped></style>
