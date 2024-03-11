<script setup lang="ts">
import { ref, watch } from 'vue';

const metric = {
    system: 'metric',
    weight: 'kg',
    height: 'cm'
};

const imperial = {
    system: 'imperial',
    weight: 'lb',
    height: 'in'
};

const unitsData = JSON.parse(localStorage.getItem('units') || 'null');
const units = ref(unitsData ? unitsData : metric);

function changeUnits() {
    units.value = units.value.system === 'metric' ? imperial : metric;
    
    localStorage.setItem('units', JSON.stringify(units.value));
}

const emit = defineEmits();

watch(units, (newUnits) => {
    emit('update:modelValue', newUnits);
});
</script>

<template>
  <div class="units-switch switch">
    <label for="units">Units:</label>
    <button id="units" @click="changeUnits()">{{ units['system'] }}</button>
  </div>
</template>

<style scoped>
</style>