
<template>
  <div class="bg-white relative border rounded-lg">
    <h1 class="text-2xl font-bold p-4">AktivBo</h1>

    <!-- Filter and Sort Controls -->
    <div class="flex items-center justify-between p-4">
      <!-- Dropdown to filter by project type -->
      <div>
        <label for="surveyType" class="mr-2">Undersökningstyp:</label>
        <select v-model="filterProjectType" id="surveyType" class="border p-2">
          <option value="all">All</option>
          <option value="Felanmälan">Felanmälan</option>
          <option value="Utflytt">Utflytt</option>
          <option value="Inflytt">Inflytt</option>
          <option value="CSC Lokal">CSC Lokal</option>
          <option value="CSC Bostad">CSC Bostad</option>
        </select>
      </div>

      <!-- Checkbox to filter by favorites -->
      <div class="ml-4">
        <label>
          <input type="checkbox" v-model="showFavorites" />
          Show Favorites Only
        </label>
      </div>

      <!-- Button to toggle sorting order by respondent count -->
      <div class="ml-4">
        <label @click="toggleSortOrder" style="cursor: pointer;">
          Sortering av respondenter
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
          <th class="px-4 py-3">Favorit</th>
          <th class="px-4 py-3">
            <span class="sr-only">View Details</span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="project in filteredAndSortedProjects" :key="project.id" @click="viewDetails(project)" class="border-b">
          <td class="px-4 py-3 font-small text-grey-900">{{ project.project_name }} </td>
          <td class="px-4 py-3 font-small text-grey-900">{{ project.project_status }} </td>
          <td class="px-4 py-3 font-small text-grey-900">{{ project.survey_type}} </td>
          <td class="px-4 py-3 font-small text-grey-900">{{ project.respondent_count }} </td>
          <td class="px-4 py-3 font-small text-grey-900">{{ project.answer_rate_latest }} </td>
          <td class="px-4 py-3 font-small text-grey-900">{{ project.integration }} </td>
          <td class="px-4 py-3 font-small text-grey-900">{{ project.date_start }} </td>
          <td class="px-4 py-3 font-small text-grey-900">{{ project.date_end }} </td>
          <td class="border p-2">
            <button @click.stop="toggleFavorite(project.project_id)">
              {{ favoriteProjects.has(project.project_id) ? '★' : '☆' }}
            </button>
          </td>
          <td class="px-4 py-3 flex items-center justify-end">
            <button @click="viewDetails(project)"> ></button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  
</template>


<script setup>
import { ref, onMounted, computed } from 'vue';

// Reactive variables for the data, filter, and sort state
const projects = ref([]); // Stores the projects data
const filterProjectType = ref('all'); // Default: 'all' (shows all projects)
const sortOrder = ref('asc'); // Default: ascending order
const favoriteProjects = ref(new Set()); // Store the favorite projects
const showFavorites = ref(false); // Boolean to toggle favorite filter

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
  console.log('Current sort order:', sortOrder.value); // Kontrollera om den byter
};

// Toggle favorite for a project
const toggleFavorite = (projectId) => {
  if (favoriteProjects.value.has(projectId)) {
    favoriteProjects.value.delete(projectId);
  } else {
    favoriteProjects.value.add(projectId);
  }
};

const filteredAndSortedProjects = computed(() => {
  // Filter projects based on selected project_type
  let filteredProjects = filterProjectType.value === 'all'
    ? projects.value // If 'all' is selected, show all projects
    : projects.value.filter(project => project.survey_type === filterProjectType.value);

  // Filter by favorites if the "Show Favorites" checkbox is checked
  if (showFavorites.value) {
    filteredProjects = filteredProjects.filter(project => favoriteProjects.value.has(project.project_id));
  }

  // Sort the filtered projects ONLY by respondent_count
  return filteredProjects.sort((a, b) => {
    const countA = parseInt(a.respondent_count, 10); // Ensure respondent_count is a number
    const countB = parseInt(b.respondent_count, 10);

    // Sort ascending or descending based on sortOrder
    return sortOrder.value === 'asc'
      ? countA - countB // Ascending order
      : countB - countA; // Descending order
  });
});


// Cardview/ modal
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



