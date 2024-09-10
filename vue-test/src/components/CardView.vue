<template>
    <div v-if="selectedItem" class="max-w-sm rounded overflow-hidden shadow-lg bg-white p-4 mt-6">
      <h2 class="text-xl font-semibold mb-2">{{ selectedItem.survey_type }}</h2>
      <p class="text-gray-700 mb-2">Svarsprocent: {{ selectedItem.answer_rate_latest}}</p>
      <p class="text-gray-700">Antal respondenter: {{ selectedItem.respondent_count }}</p>
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
  </script>


<!-- <template>
    <div>
      <h1>Project Details</h1>
      <div v-if="selectedItem" class="card">
        <h2>{{ selectedItem.project_name }}</h2>
        <p>Type: {{ selectedItem.project_type }}</p>
        <p>Respondents: {{ selectedItem.respondent_count }}</p>
      </div>
      <div v-else>
        <p>No project selected. Click on "Details" to view a project.</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    selectedItem: Object
  });
  </script>
  
  <style scoped>
  .card {
    border: 1px solid #ddd;
    padding: 16px;
    border-radius: 8px;
    background-color: #f9f9f9;
    margin-top: 20px;
  }
  </style> -->