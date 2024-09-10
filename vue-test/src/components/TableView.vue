<script setup>
import { ref, onMounted, computed } from 'vue';

// Reactive variables for the data, filter, and sort state
const projects = ref([]); // Stores the projects data
const filterProjectType = ref('all'); // Default: 'all' (shows all projects)
const sortOrder = ref('asc'); // Default: ascending order

// Simulate fetching data from a local JSON file (like calling an internal API)
async function fetchProjects() {
  try {
    const response = await fetch('/src/aktivbo.json'); // Simulate API call
    projects.value = await response.json(); // Assign data to reactive projects
  } catch (error) {
    console.error('Error fetching projects:', error);
  }
}

// Fetch data when the component is mounted
onMounted(fetchProjects);

// Toggle between ascending and descending order
const toggleSortOrder = () => {
  sortOrder.value = sortOrder.value === 'asc' ? 'desc' : 'asc';
};

// Computed property to filter and sort projects
const filteredAndSortedProjects = computed(() => {
  // Step 1: Filter projects based on selected project_type
  let filteredProjects = filterProjectType.value === 'all'
    ? projects.value // If 'all' is selected, show all projects
    : projects.value.filter(project => project.survey_type === filterProjectType.value);

  // Step 2: Sort the filtered projects by respondent_count
  return filteredProjects.sort((a, b) => {
    return sortOrder.value === 'asc'
      ? a.respondent_count - b.respondent_count // Ascending order
      : b.respondent_count - a.respondent_count; // Descending order
  });
});

import { defineEmits, defineProps } from 'vue';

// Define props and emits
const props = defineProps({
  items: Array
});
const emit = defineEmits(['showDetails']);

// Method to emit the selected item
const viewDetails = (project) => {
  emit('showDetails', project);
};
</script>

<template>
  <div class="bg-white relative border rounded-lg">
    <h1>AktivBo</h1>
    <div class="flex items-center justify-between">
        <!-- Dropdown to filter by project type -->
        <div class="px-4 py-3">
          <label for="surveyType">Undersökningstyp:</label>
          <select v-model="filterProjectType" id="surveyType">
            <option value="all">All</option>
            <option value="Felanmälan">Felanmälan</option>
            <option value="Utflytt">Utflytt</option>
            <option value="Inflytt">Inflytt</option>
            <option value="CSC Lokal">CSC Lokal</option>
            <option value="CSC Bostad">CSC Bostad</option>
          </select>
        </div>
      

      <!-- Button to toggle sorting order by respondent count -->
      <div class="px-4 py-3">
        <label @click="toggleSortOrder" style="cursor: pointer;">
          Sort by Respondent Count
          <span v-if="sortOrder === 'asc'">⬆️</span>
          <span v-else>⬇️</span>
        </label>
      </div>
   
    </div>
  

    <!-- Display filtered and sorted projects in a table -->
      <table class="w-full text-sm text-left text-gray-500">
            <thead class="text-sm text-gray-700 bg-gray-50">
                <tr>
                    <th class="px-4 py-3">Projektnamn</th>
                    <th class="px-4 py-3">Projektstatus</th>
                    <th class="px-4 py-3">Undersökningstyp</th>
                    <th class="px-4 py-3">Antal respondenter</th>
                    <th class="px-4 py-3">Svarsprocent</th>
                    <th class="px-4 py-3">Integration</th>
                    <th class="px-4 py-3">Startdatum</th>
                    <th class="px-4 py-3">Slutdatum</th>
                    <th class="px-4 py-3">
                        <span class="sr-only">></span>
                    </th>

                </tr>
            </thead>
      <tbody>
        <tr v-for="project in filteredAndSortedProjects" :key="project.id" @click="selectItem(item)" class="border-b">
                    <td class="px-4 py-3 font-small text-grey-900">{{ project.project_name }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ project.project_status }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ project.survey_type}} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ project.respondent_count }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ project.answer_rate_latest }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ project.integration }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ project.date_start }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ project.date_end }} </td>
                    <td class="px-4 py-3 flex items-center justify-end">
                      <button @click="viewDetails(project)">></button>
                    </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>