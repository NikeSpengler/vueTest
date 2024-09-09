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
    <div>
        <table>
            <thead>
                <tr>
                    <th>Projektnamn</th>
                    <th>Projektstatus</th>
                    <th>Undersökningstyp</th>
                    <th>Antal respondenter</th>
                    <th>Svarsprocent</th>
                    <th>Integration</th>
                    <th>Startdatum</th>
                    <th>Slutdatum</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in data" :key="item.id"> 
                    <td>{{ item.project_name }} </td>
                </tr>
            </tbody>
            
        </table>
    </div>
 
</template>