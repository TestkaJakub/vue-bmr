<script setup lang="ts">
import { ref, toRaw, watch} from 'vue';

import ThemeSwitch from './components/ThemeSwitch.vue';
import UnitsSwitch from './components/UnitsSwitch.vue';
import WeightInput from './components/WeightInput.vue';

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

watch(weights, (newUnits) => {
    console.log(toRaw(newUnits));
});

</script>

<template>
  <ThemeSwitch/>
  <div class="main">
    <h1>BMRrro.com</h1>
    <UnitsSwitch v-model="units"/>
    <WeightInput :weightUnit="toRaw(units)['weight']" v-model="weights"/>
    <!-- <label for="weight">weight in {{ toRaw(units)['weight'] }}</label>
    <input type="number" name="weight" id="weight"> -->
  </div>

</template>

<style scoped>
</style>
