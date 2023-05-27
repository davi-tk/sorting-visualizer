<script setup lang="ts">
import { ref, Ref, watch } from 'vue';
import { random } from 'lodash';
import { NSlider, NInputNumber, NButton } from 'naive-ui';
import ArrayView from './components/ArrayView.vue';
import Options from './components/Options.vue';

const min: number = 50
const length: Ref<number> = ref(min)
const max : number = length.value * 2
const selected : Ref<boolean> = ref(false)
const algo : Ref<Function> = ref(() => {})
 
const randomArray = (length: number, min: number, max: number): number[] => [...new Array(length)].map(() => random(min / 2, max))

const array: Ref<number[]> = ref(randomArray(length.value, min, max))

watch(length, () => array.value = randomArray(length.value, min, max))

const sortArray = (array: number[], fn : Function): number[] => fn(array)

const listen = (algorithm: Function) : void => {
  algo.value = algorithm
  selected.value = true
}

</script>

<template>
  <section id="controllers" class="grid grid-flow-col grid-cols-10 items-end gap-10">
    <div id="slider" class="pt-4 pl-4 col-span-2">
      <h3 class="text-lg">Array size</h3>
      <n-slider :min=min v-model:value="length" :step="2" :max="200" class="my-4" />
      <n-input-number :min="min" v-model:value="length" :max="200" size="large" />
    </div>
    <NButton @click="array = randomArray(length, min, max)" type="primary" ghost size="large" class="col-span-2">Generate New Array</NButton>
    <Options @algorithm= "listen"/>
    <NButton @click="sortArray(array, algo)" type="info" ghost size="large" :disabled="!selected">Sort!</NButton>
  </section>
  <ArrayView :length="length" :array="array"/>
</template>

<style scoped></style>
