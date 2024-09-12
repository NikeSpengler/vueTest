<template>
    <div v-if="selectedItem" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center" @click="closeModal">
      <div class="bg-white p-6 rounded-lg shadow-lg max-w-sm relative" @click.stop>
        <!-- Close Button -->
        <span class="absolute top-2 right-2 text-black hover:text-gray-500 text-lg pr-2" @click="closeModal">
          &times;
        </span>
  
        <!-- Modal Content -->
        <h2 class="text-sky-900 pt-10 text-3xl font-semibold mb-2">{{ selectedItem.survey_type }}</h2>
        <h1 class="t text-sky-900 mb-2 py-6"> {{ selectedItem.answer_rate_latest }} %</h1>
        <div class="flex items-center justify-between pb-10">
          <p class="text-gray-700 px-10">Svarsprocent: {{ selectedItem.answer_rate_latest }}</p>
          <p class="text-gray-700 pr-10">Antal respondenter: {{ selectedItem.respondent_count }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineEmits, defineProps } from 'vue';
  
  // Define props for the selected item
  const props = defineProps({
    selectedItem: Object
  });
  
  // Define emits to communicate with the parent component
  const emit = defineEmits(['close']);
  
  // Function to close the modal
  const closeModal = () => {
    emit('close');
  };
  </script>
  
  <style scoped>
  /* Ensure the modal is on top of other content */
  .fixed {
    z-index: 1000; /* High z-index to ensure it's above other content */
  }
  
  /* Optional: Center the modal and add a max-width */
  .max-w-sm {
    max-width: 500px; /* Adjust based on your design */
  }
  
  /* Close button styling */
  .text-lg {
    font-size: 1.25rem; /* Size of the close button */
  }
  </style>





