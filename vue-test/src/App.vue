<template>
  <div>
    <TableView :items="items" @showDetails="handleShowDetails" />
    <CardView :selectedItem="selectedItem" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import TableView from './components/TableView.vue';
import CardView from './components/CardView.vue';
import projects from './aktivbo.json'; // Example JSON file

const items = ref(projects);
const selectedItem = ref(null);

// Handle showing details when a "Details" button is clicked
const handleShowDetails = (item) => {
  selectedItem.value = item;
};
</script>
