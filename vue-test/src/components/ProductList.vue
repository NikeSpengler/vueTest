<template>
    <div>
        <h1 class="text-4xl font-bold py-12 p-4 text-sky-950">AktivBo Analytics</h1>
        <div class="bg-white relative border rounded-lg">
        <!-- <h1 class="text-4xl font-bold p-4 text-sky-950">AktivBo</h1> -->
    
        <!-- Filter and Sort Controls -->
        <div class="flex text-sm items-center justify-between p-4">
            <!-- Dropdown to filter by project type -->
            <div>
            <label for="surveyType" class="mr-2 text-sky-900">Undersökningstyp:</label>
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
            <div class="ml-4 text-sky-900">
            <label>
                <input type="checkbox" v-model="showFavorites" />
                Favoriter
            </label>
            </div>
    
            <!-- Button to toggle sorting order by respondent count -->
            <div class="ml-4 text-sky-900">
            <label @click="toggleSortOrder" style="cursor: pointer;">
                Sortera respondenter
                <span v-if="sortOrder === 'asc'">⇅</span>
                <span v-else>⇅</span>
            </label>
            </div>
        </div>
    
        <!-- Display filtered and sorted projects in a table -->
        <table class="w-full text-sm text-left text-gray-500">
            <thead class="text-sm text-sky-900 bg-gray-50">
            <tr>
                <th class="px-4 py-3">Projektnamn</th>
                <th class="px-4 py-3">Projektstatus</th>
                <th class="px-4 py-3">Undersökningstyp</th>
                <th class="px-4 py-3">Respondenter</th>
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
            <tr v-for="project in filteredAndSortedProjects" :key="project.id" class="border-b hover:bg-gray-50">
                <td class="px-4 py-3 font-small text-grey-900">{{ project.project_name }} </td>
                <td class="px-4 py-3 font-small text-grey-900">{{ project.project_status }} </td>
                <td class="px-4 py-3 font-small text-grey-900">{{ project.survey_type }} </td>
                <td class="px-4 py-3 font-small text-grey-900">{{ project.respondent_count }} </td>
                <td class="px-4 py-3 font-small text-grey-900">{{ project.answer_rate_latest }} </td>
                <td class="px-4 py-3 font-small text-grey-900">{{ project.integration }} </td>
                <td class="px-4 py-3 font-small text-grey-900">{{ project.date_start }} </td>
                <td class="px-4 py-3 font-small text-grey-900">{{ project.date_end }} </td>
                <td class="px-4 py-3 font-small text-grey-900 hover:text-grey-100 hover:cursor-pointer">
                <span @click.stop="toggleFavorite(project.project_id)">
                    {{ favoriteProjects.has(project.project_id) ? '★' : '☆' }}
                </span>
                </td>
                <td class="px-4 py-3 font-small text-grey-900 hover:text-grey-100 hover:cursor-pointer">
                <span @click="viewDetails(project)">></span>
                </td>
            </tr>
            </tbody>
        </table>
    
        <!-- Modal -->
        <ProductCard
            v-if="selectedProject"
            :selectedItem="selectedProject"
            :isVisible="!!selectedProject"
            @close="selectedProject = null"
        />
        </div>
    </div>
   
  </template>
  
  <script setup>
  import { ref, onMounted, computed } from 'vue';
//   import ProductCardModal from './ProductCardModal.vue'; // Import the CardView component
import ProductCard from './ProductCard.vue';
  
  // Reactive variables for the data, filter, and sort state
  const projects = ref([]);
  const filterProjectType = ref('all');
  const sortOrder = ref('asc');
  const favoriteProjects = ref(new Set());
  const showFavorites = ref(false);
  const selectedProject = ref(null);
  
  // Simulate fetching data from a local JSON file (like calling an internal API)
  async function fetchProjects() {
    try {
      const response = await fetch('/src/aktivbo.json');
      projects.value = await response.json();
    } catch (error) {
      console.error('Error fetching projects:', error);
    }
  }
  
  // Fetch data when the component is mounted
  onMounted(fetchProjects);
  
  const toggleSortOrder = () => {
    sortOrder.value = sortOrder.value === 'asc' ? 'desc' : 'asc';
  };
  
  const toggleFavorite = (projectId) => {
    if (favoriteProjects.value.has(projectId)) {
      favoriteProjects.value.delete(projectId);
    } else {
      favoriteProjects.value.add(projectId);
    }
  };
  
  const filteredAndSortedProjects = computed(() => {
    let filteredProjects = filterProjectType.value === 'all'
      ? projects.value
      : projects.value.filter(project => project.survey_type === filterProjectType.value);
  
    if (showFavorites.value) {
      filteredProjects = filteredProjects.filter(project => favoriteProjects.value.has(project.project_id));
    }
  
    return filteredProjects.sort((a, b) => {
      const countA = parseInt(a.respondent_count, 10);
      const countB = parseInt(b.respondent_count, 10);
  
      return sortOrder.value === 'asc' ? countA - countB : countB - countA;
    });
  });
  
  const viewDetails = (project) => {
    selectedProject.value = project;
  };
  </script>
  
  

    

    