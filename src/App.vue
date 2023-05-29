<script setup lang="ts">
import { ref, Ref, watch } from 'vue';
import {random } from 'lodash';
import { NSlider, NInputNumber, NButton } from 'naive-ui';
import ArrayView from './components/ArrayView.vue';
import Options from './components/Options.vue';

const min: number = 10
const length: Ref<number> = ref(min)
const max = 150
const selected : Ref<boolean> = ref(false)
const algo : Ref<Function> = ref(() => {})
const n : Ref<number> = ref(-1)
const m : Ref<number> = ref(-1)
const done : Ref<boolean> = ref(false)
const delay : Ref<number> = ref(0.1)
 
const randomArray = (length: number, min: number, max: number): number[] => {
  done.value = false
  return [...new Array(length)].map(() => random(min / 2, max))
}
const array: Ref<number[]> = ref(randomArray(length.value, min, max))

watch(length, () => array.value = randomArray(length.value, min, max))

const sortArray = (array: number[], fn : Function): number[] => {

  const speed = 300 - delay.value - 0.1

  return fn(array, n, m, selected, done, speed)
} 

const listen = (algorithm: Function) : void => {
  algo.value = algorithm
  selected.value = true
}



</script>

<template>
  <section id="controllers" class="grid grid-flow-col grid-cols-10 items-end gap-10">
    <div id="array-size" class="pt-4 pl-4">
      <h3 class="text-lg">Array size</h3>
      <n-slider :min=min v-model:value="length" :step="2" :max="max" class="my-4" />
      <n-input-number :min="min" v-model:value="length" :max="max" size="large" />
    </div>
    <div id="speed" class="pt-4 pl-4 ">
      <h3 class="text-lg">Speed</h3>
      <n-slider :min=0.1 v-model:value="delay" :step="25" :max="300" class="my-4" />
      <n-input-number :min="0.1" v-model:value="delay" :max="300" size="large" />
    </div>
    <NButton @click="array = randomArray(length, min, max)" type="primary" ghost size="large" class="col-span-2">Generate New Array</NButton>
    <Options @algorithm= "listen"/>
    <NButton @click="sortArray(array, algo)" type="info" ghost size="large" :disabled="!selected">Sort!</NButton>
  </section>
  <ArrayView :done="done" :length="length" :array="array" :n="n" :m="m"/>
</template>

<style scoped></style>
