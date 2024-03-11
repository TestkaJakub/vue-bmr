<script setup lang="ts">
import { ref, watch } from 'vue';

import ThemeSwitch from './components/ThemeSwitch.vue';
import UnitsSwitch from './components/UnitsSwitch.vue';

const units = ref(localStorage.getItem('units') || 'metric');

watch(units, (newUnits) => {
    console.log(newUnits)
});
</script>

<template>
  <ThemeSwitch/>
  <div class="main">
    <h1>BMRrro.com</h1>
    <UnitsSwitch v-model="units"/>
  </div>

</template>

<style scoped>
</style>
