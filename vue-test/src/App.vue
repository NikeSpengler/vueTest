<!-- <template>
  <div>
    <ProjectList />
    <ProjectCardModal />
  </div>
</template>

<script setup>
import ProjectList from './components/ProductList.vue';
import ProjectCardModal from './components/ProductCardModal.vue';
</script> -->


<template>
  <div>
    <ProductList :items="items" @showDetails="handleShowDetails" />
    <ProductCardModal :selectedItem="selectedItem" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
// import TableView from './components/TableView.vue'
import ProductList from './components/ProductList.vue';
import ProductCardModal from './components/ProductCardModal.vue';
// import CardView from './components/CardView.vue';
import projects from './aktivbo.json'; // Example JSON file

const items = ref(projects);
const selectedItem = ref(null);

// Handle showing details when a "Details" button is clicked
const handleShowDetails = (item) => {
  selectedItem.value = item;
};
</script>
