<script setup lang="ts">
import { ref, Ref, watch } from 'vue';
import {random } from 'lodash';
import { NSlider, NInputNumber, NButton } from 'naive-ui';
import ArrayView from './components/ArrayView.vue';
import Options from './components/Options.vue';

const nope = () => 'nope'

const min: number = 10
const length: Ref<number> = ref(min)
const max = 300
const selected : Ref<boolean> = ref(false)
const algo : Ref<Function> = ref(nope)
const n : Ref<number> = ref(-1)
const m : Ref<number> = ref(-1)
const done : Ref<boolean> = ref(false)
const positioned : Ref<number[]> = ref([])
const delay : Ref<number> = ref(0)


const randomArray = (length: number, min: number, max: number): number[] => {
  return [...new Array(length)].map(() => random(min / 2, max))
}

const newArray = (length: number, min: number, max: number): number[] => {
  positioned.value = []
  done.value = false
  if(!(algo.value() == 'nope'))selected.value = true
  return randomArray(length, min, max)
}

const array: Ref<number[]> = ref(randomArray(length.value, min, max))

watch(length, () => {
  array.value = randomArray(length.value, min, max)
  positioned.value = []
})

const sortArray = async ( fn : Function): Promise<void> => {

  done.value = true
  selected.value = false
  array.value =  await (fn(array.value, n, m, delay.value, positioned))
  done.value = false

} 

const listen = (algorithm: Function) : void => {
  algo.value = algorithm
  if(positioned.value.length == 0)
  selected.value = true
}


</script>

<template>
  <section id="controllers" class="grid grid-flow-col grid-cols-7 items-end gap-10 w-2/3 m-auto">
    <div id="array-size" class="pt-4">
      <h3 class="text-lg">Array size</h3>
      <n-slider :min=min v-model:value="length" :step="2" :max="max" class="my-4" :disabled="done" />
      <n-input-number :min="min" v-model:value="length" :max="max" size="large" :disabled="done" />
    </div>
    <div id="delay" class="pt-4">
      <h3 class="text-lg">Delay between swaps</h3>
      <n-slider :min="0" v-model:value="delay" :step="2" :max="100" class="my-4" :disabled="done" />
      <n-input-number :min="0" v-model:value="delay" :max="100" size="large" :disabled="done" />
    </div>
    <Options @algorithm= "listen" :disabled="done"/>
    <NButton @click="array = newArray(length, min, max)" type="primary" ghost size="large" class="col-span-2" :disabled="done">Generate New Array</NButton>
    <NButton @click="sortArray(algo)" type="info" ghost size="large" :disabled="!selected">Sort!</NButton>
  </section>
  <ArrayView :positioned="positioned" :length="length" :array="array" :n="n" :m="m"/>
</template>

<style scoped></style>
