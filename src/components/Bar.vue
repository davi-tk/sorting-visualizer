<template>
    <div :style="barStyle">
        {{ size }}
    </div>
</template>

<script setup lang="ts">

const props = defineProps<{
    size : number
}>()

const barStyle = {
    height: `${props.size + 2}rem`,
    width: '2rem',
    backgroundColor : 'aliceblue',
    color: 'red',
}

</script>

<style scoped>

</style>