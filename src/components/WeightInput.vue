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
    emit('update:modelValue', { kg: newWeightKg, lb: weightLb.value});
});

watch(weightLb, (newWeightLb) => {
    emit('update:modelValue', { kg: weightKg.value, lb: newWeightLb });
});
</script>

<template>
    <div class="bmr-input">
        <label for="weight">Weight in <span>{{ props.weightUnit }}</span>:</label>
        <input v-if="props.weightUnit == 'kg'" type="number" name="weight" id="weight" v-model="weightKg">
        <input v-else-if="props.weightUnit == 'lb'" type="number" name="weight" id="weight" v-model="weightLb">
    </div>
</template>

<style scoped>
</style>