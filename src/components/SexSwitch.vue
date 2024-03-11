<script setup lang="ts">
import { ref, watch } from 'vue';

const currentSex = ref(localStorage.getItem('sex') || 'female');

function changeUnits() {
    currentSex.value = currentSex.value === 'female' ? 'male' : 'female';
    
    localStorage.setItem('sex', currentSex.value);
}

const emit = defineEmits();

watch(currentSex, (newSex) => {
    emit('update:modelValue', newSex);
});
</script>

<template>
  <div class="units-switch switch">
    <label for="units">Sex:</label>
    <button id="units" @click="changeUnits()">{{ currentSex }}</button>
  </div>
</template>

<style scoped>
</style>