<script>
import aktivBo from '../aktivbo.json'

export default {
  data() {
    return { 
      data: aktivBo 
    }
  }
 }
</script>


<template>
    <div class="bg-white relative border rounded-lg">
        <table class="w-full test sm text-left text-grey-500">
            <thead class="text-xs text-gray-700 uppercase bg-grey-50">
                <tr>
                    <th class="px-4 py-3">Projektnamn</th>
                    <th class="px-4 py-3">Projektstatus</th>
                    <th class="px-4 py-3">Undersökningstyp</th>
                    <th class="px-4 py-3">Antal respondenter</th>
                    <th class="px-4 py-3">Svarsprocent</th>
                    <th class="px-4 py-3">Integration</th>
                    <th class="px-4 py-3">Startdatum</th>
                    <th class="px-4 py-3">Slutdatum</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in data" :key="item.id"> 
                    <td class="px-4 py-3 font-medium text-grey-900">{{ item.project_name }} </td>
                    <td class="px-4 py-3 font-medium text-grey-900">{{ item.project_status }} </td>
                    <td class="px-4 py-3 font-medium text-grey-900">{{ item.project_type}} </td>
                    <td class="px-4 py-3 font-medium text-grey-900">{{ item.respondent_count }} </td>
                    <td class="px-4 py-3 font-medium text-grey-900">{{ item.answer_rate_latest }} </td>
                    <td class="px-4 py-3 font-medium text-grey-900">{{ item.integration }} </td>
                    <td class="px-4 py-3 font-medium text-grey-900">{{ item.date_start }} </td>
                    <td class="px-4 py-3 font-medium text-grey-900">{{ item.date_end }} </td>
                </tr>
            </tbody>
            
        </table>
    </div>
 
</template>

<style>
.background_box {
    background-color: white;
    position: relative;
    border-radius: 20%;
    

}

table {
    background-color: white;

}

</style>