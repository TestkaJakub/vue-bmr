<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps({
    heightUnit: {
        type: String,
        required: true
    }
});

const heightCm = ref(null);
const heightIn = ref(null);

const emit = defineEmits();

watch(heightCm, (newHeightCm) => {
    emit('update:modelValue', { cm: newHeightCm, in: heightIn.value});
});

watch(heightIn, (newHeightIn) => {
    emit('update:modelValue', { cm: heightCm.value, in: newHeightIn });
});
</script>

<template>
    <div class="bmr-input">
        <label for="height">Height in {{ props.heightUnit }}:</label>
        <input v-if="props.heightUnit == 'cm'" type="number" name="height" id="height" v-model="heightCm">
        <input v-else-if="props.heightUnit == 'in'" type="number" name="height" id="height" v-model="heightIn">
    </div>
</template>

<style scoped>
</style>