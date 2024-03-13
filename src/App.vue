<!-- 
  footer is not centered
  labels are not centered
 -->

<script setup lang="ts">
import { ref, toRaw, watch} from 'vue';

import ThemeSwitch from './components/ThemeSwitch.vue';
import UnitsSwitch from './components/UnitsSwitch.vue';
import SexSwitch from './components/SexSwitch.vue';
import WeightInput from './components/WeightInput.vue';
import HeightInput from './components/HeightInput.vue';
import AgeInput from './components/AgeInput.vue';
import KofiButton from './components/KofiButton.vue';

const metric = {
    system: 'metric',
    weight: 'kg',
    height: 'cm'
};

const unitsData = JSON.parse(localStorage.getItem('units') || 'null');
const units = ref(unitsData ? unitsData : metric);

const sex = ref(localStorage.getItem('sex') || 'female');

const weights = ref({
    kg: 0,
    lb: 0
});

const heights = ref({
    cm: 0,
    in: 0
});

const age = ref(0);

const bmr = ref(0);

function calculateBmr() {
  if (checkIfValue(age.value) === false)
    return 0;
  if (units.value.system === 'metric') {
    if(checkIfValue(weights.value.kg) === false)
      return 0;
    if(checkIfValue(heights.value.cm) === false)
      return 0;
    return 10 * weights.value.kg + 6.25 * heights.value.cm - 5 * age.value + (sex.value === 'male' ? 5 : -161);
  } else {
    if(checkIfValue(weights.value.lb) === false)
      return 0;
    if(checkIfValue(heights.value.in) === false)
      return 0;
    return 10 * weights.value.lb + 6.25 * heights.value.in - 5 * age.value + (sex.value === 'male' ? 5 : -161);
  }
}

function checkIfValue(value : any) {
  if (value === 0 || null || undefined || isNaN(value) || value === '')
    return false;
  return true;
}

watch([units, weights, heights, age, sex], () => {
  bmr.value = calculateBmr();
});
</script>

<template>
  <ThemeSwitch/>
  <div class="main">
    <img src="./assets/bmrrro.png" alt="BMRrro logo" class="logo" width="200px"/>
    <div class="controls">
      <UnitsSwitch v-model="units"/>
      <SexSwitch v-model="sex"/>
    </div>
    
    <div class="bmr" v-if="bmr>0">
      <h2>BMR: {{ bmr }}</h2>
    </div>
    
    <AgeInput v-model="age"/>
    <HeightInput :heightUnit="toRaw(units)['height']" v-model="heights"/>
    <WeightInput :weightUnit="toRaw(units)['weight']" v-model="weights"/>
    
  </div>
  <footer>
    <p>created by <a target="_blank" href="https://github.com/TestkaJakub">Jakub Testka</a></p>
    <KofiButton/>
  </footer>

</template>

<style scoped>
</style>
