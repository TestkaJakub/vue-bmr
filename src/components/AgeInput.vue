<script setup lang="ts">
import { ref, watch } from 'vue';

const age = ref(null);

const emit = defineEmits();

watch(age, (newAge) => {
    emit('update:modelValue', newAge);
});
</script>
<template>
    <div class="bmr-input">
        <label for="age">Age:</label>
        <input type="number" name="age" id="age" v-model="age">
    </div>
</template>
<style scoped>
</style>