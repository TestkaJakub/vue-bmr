<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps({
    weightUnit: {
        type: String,
        required: true
    }
});

const weightKg = ref(null);
const weightLb = ref(null);

const emit = defineEmits();

watch(weightKg, (newWeightKg) => {
    emit('update:modelValue', { kg: newWeightKg, lb: newWeightKg? newWeightKg * 2.20462 : null});
});

watch(weightLb, (newWeightLb) => {
    emit('update:modelValue', { kg: newWeightLb ? newWeightLb / 2.20462 : null, lb: newWeightLb });
});
</script>

<template>
    <div>
        <label for="weight">weight in {{ props.weightUnit }}</label>
        <input v-if="props.weightUnit == 'kg'" type="number" name="weight" id="weight" v-model="weightKg">
        <input v-else-if="props.weightUnit == 'lb'" type="number" name="weight" id="weight" v-model="weightLb">
    </div>
</template>

<style scoped>
</style>