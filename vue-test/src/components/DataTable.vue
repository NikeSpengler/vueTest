<script>

import projects from '../aktivbo.json'
import { ref, computed } from 'vue';


export default {
  data() {
    return { 
      data: projects 
    }
  }
 }


// Reactive variable for the selected project type
const filterProjectType = ref('all'); // Default is 'all' to show all projects

// Computed property to filter the JSON data based on the selected project type
const filteredProjects = computed(() => {
  return filterProjectType.value === 'all'
    ? projects // If 'all' is selected, return all projects
    : projects.filter(item => item.project_type === filterProjectType.value);
});

</script>


<template>
    <div class="bg-white relative border rounded-lg">
        <div class="flex items-center justify-between">
          
            <!--Sort button-->


            
             <!-- Dropdown to select the project type for filtering -->
             <div>
                <label for="projectType">Undersökningstyp:</label>
                <select v-model="filterProjectType" id="projectType">
                    <option value="all">All</option>
                    <option value="Standard project">Standard project</option>
                    <option value="Continuous project">Continuous project</option>
                </select>
             </div>
              
          
    

   

        </div>
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
                <tr v-for="item in filteredProjects" :key="item.id" class="border-b"> 
                    <td class="px-4 py-3 font-small text-grey-900">{{ item.project_name }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ item.project_status }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ item.project_type}} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ item.respondent_count }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ item.answer_rate_latest }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ item.integration }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ item.date_start }} </td>
                    <td class="px-4 py-3 font-small text-grey-900">{{ item.date_end }} </td>
                    <td class="px-4 py-3 flex items-center justify-end">
                        <a href="#" class="text-indigo-500 hover:underline">></a>
                    </td>
                </tr>
            </tbody>
            
        </table>
    </div>
 
</template>

<style>


</style>