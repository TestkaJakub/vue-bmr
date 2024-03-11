<script setup lang="ts">
import { ref, toRaw, watch} from 'vue';

import ThemeSwitch from './components/ThemeSwitch.vue';
import UnitsSwitch from './components/UnitsSwitch.vue';
import SexSwitch from './components/SexSwitch.vue';
import WeightInput from './components/WeightInput.vue';
import HeightInput from './components/HeightInput.vue';

const metric = {
    system: 'metric',
    weight: 'kg',
    height: 'cm'
};

const unitsData = JSON.parse(localStorage.getItem('units') || 'null');
const units = ref(unitsData ? unitsData : metric);

const weights = ref({
    kg: 0,
    lb: 0
});

const heights = ref({
    cm: 0,
    in: 0
});

watch(heights, (newUnits) => {
    console.log(toRaw(newUnits));
});

watch(weights, (newUnits) => {
    console.log(toRaw(newUnits));
});

</script>

<template>
  <ThemeSwitch/>
  <div class="main">
    <h1>BMRrro.com</h1>
    <UnitsSwitch v-model="units"/>
    <SexSwitch />
    <WeightInput :weightUnit="toRaw(units)['weight']" v-model="weights"/>
    <HeightInput :heightUnit="toRaw(units)['height']" v-model="heights"/>
  </div>

</template>

<style scoped>
</style>
