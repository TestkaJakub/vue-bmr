<script setup lang="ts">
import { ref, watch } from 'vue';
    
const units = ref(localStorage.getItem('units') || 'metric');

function changeUnits(){
  units.value = units.value === 'metric' ? 'imperial' : 'metric';
  localStorage.setItem('units', units.value);
}

const emit = defineEmits();

watch(units, (newUnits) => {
    emit('update:modelValue', newUnits);
});
</script>

<template>
  <div class="units-switch">
    <label for="units">Units:</label>
    <button id="units" @click="changeUnits()">{{ units }}</button>
  </div>
</template>

<style scoped>
</style>