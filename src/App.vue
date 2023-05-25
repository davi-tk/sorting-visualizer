<script setup lang="ts">
import { ref, Ref, watch } from 'vue';
import { random } from 'lodash';
import { NSlider, NInputNumber } from 'naive-ui';
import ArrayView from './components/ArrayView.vue';

const min: number = 50
const length: Ref<number> = ref(min)

const randomArray = (length: number, min : number, max: number): number[] => [...new Array(length)].map(() => random(min/2, max))

const array: Ref<number[]> = ref(randomArray(length.value, 50, length.value * 2))

watch(length, () => array.value = randomArray(length.value, 50,  length.value * 2))



</script>

<template>
  <section id="slider" class="w-3/12 p-4 m-auto">
    <h3 class="text-lg">Array size</h3>
    <n-slider :min=min v-model:value="length" :step="2" class="my-4" />
    <n-input-number :min="min" v-model:value="length" />
  </section>

  <ArrayView :length="length" :array="array"/>

</template>

<style scoped></style>
