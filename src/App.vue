<script setup lang="ts">
import { ref, Ref, watch } from 'vue';
import { random } from 'lodash';
import { NSlider, NInputNumber } from 'naive-ui';
import ArrayView from './components/ArrayView.vue';

const min: number = 50
const length: Ref<number> = ref(min)

const randomArray = (length: number, max: number): number[] => [...new Array(length)].map(() => random(1, max))

const array: Ref<number[]> = ref(randomArray(length.value, length.value * 2))

watch(length, () => array.value = randomArray(length.value, length.value * 2))


</script>

<template>
  <section id="slider" class="w-1/3 p-4">

    <n-slider :min=min v-model:value="length" :step="2" />
    <n-input-number :min="min" v-model:value="length" size="small" />
  </section>

  <ArrayView :length="length" :array="array"/>

</template>

<style scoped></style>
