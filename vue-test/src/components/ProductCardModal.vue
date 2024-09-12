<template>
  <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50">
    <div class="bg-white p-6 rounded-lg shadow-lg max-w-lg">
      <!-- Close Button -->
      <span class="absolute top-2 right-2 text-white hover:text-gray-50" @click="$emit('close')">✕</span>

      <!-- Card/ Modal Content -->
      <h2 class="text-sky-900 pt-10 text-3xl font-semibold mb-2">{{ selectedItem.survey_type }}</h2>
      <h1 class=" text-sky-900 mb-2 py-6">{{ selectedItem.answer_rate_latest }} % </h1>
      <div class="flex items-center justify-between p-4 pb-10">
        <p class="text-gray-700 mb-2">Svarsprocent: {{ selectedItem.answer_rate_latest }}</p>
        <p class="text-gray-700">Antal respondenter: {{ selectedItem.respondent_count }}</p>
      </div>
    </div>
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