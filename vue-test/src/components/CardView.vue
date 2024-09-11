<template>
    <div v-if="selectedItem" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center" @click="closeModal">
      <div class="bg-white p-6 rounded-lg shadow-lg max-w-sm relative" @click.stop>
        <!-- Close Button -->
        <button class="absolute top-2 right-2 text-gray-500 hover:text-gray-700 text-lg" @click="closeModal">
          &times;
        </button>
  
        <!-- Modal Content -->
        <h2 class="text-xl font-semibold mb-2">{{ selectedItem.survey_type }}</h2>
        <p class="text-xl font-semibold text-gray-700 mb-2"> {{ selectedItem.answer_rate_latest }} %</p>
        <p class="text-gray-700 mb-2">Svarsprocent: {{ selectedItem.answer_rate_latest }}</p>
        <p class="text-gray-700">Antal respondenter: {{ selectedItem.respondent_count }}</p>
      </div>
    </div>
    <div v-else class="text-gray-600 mt-6">
      <p>No project selected. Click "Details" to view project details.</p>
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



<!-- <template>
    <div v-if="selectedItem" class="max-w-sm rounded overflow-hidden shadow-lg bg-white p-4 mt-6">
      <h2 class="text-xl font-semibold mb-2">{{ selectedItem.survey_type }}</h2>
      <p class="text-gray-700 mb-2">Svarsprocent: {{ selectedItem.answer_rate_latest}}</p>
      <p class="text-gray-700">Antalespondents: {{ selectedItem.respondent_count }}</p>
    </div>
    <div v-else class="text-gray-600 mt-6">
      <p>No project selected. Click "Details" to view project details.</p>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  // Define props for the selected item
  const props = defineProps({
    selectedItem: Object
  });
  </script> -->


