<template>
  <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50">
    <div class="bg-white p-6 rounded-lg shadow-lg max-w-lg w-full">
      <button class="absolute top-2 right-2 text-gray-500 hover:text-gray-700" @click="$emit('close')">✕</button>
      <h2 class="text-3xl font-semibold mb-2">{{ selectedItem.survey_type }}</h2>
      <h1 class="text-gray-700 mb-2">{{ selectedItem.answer_rate_latest }} % </h1>
      <div class="flex items-center justify-between p-4">
        <p class="text-gray-700 mb-2">Svarsprocent: {{ selectedItem.answer_rate_latest }}</p>
        <p class="text-gray-700">Antal respondenter: {{ selectedItem.respondent_count }}</p>
      </div>
      
    </div>
  </div>
  <div v-else class="text-gray-600 mt-6">
      <p>No project selected. Click "Details" to view project details.</p>
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  selectedItem: Object,
  isVisible: Boolean
});
const emit = defineEmits(['close']);
</script>

<style scoped>
/* Add any additional styling here if needed */
</style>