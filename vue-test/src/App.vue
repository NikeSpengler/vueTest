<template>
  <div>
    <ProductList :items="items" @showDetails="handleShowDetails" />
    <ProductCard :selectedItem="selectedItem" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import ProductList from './components/ProductList.vue';
import ProductCard from './components/ProductCard.vue';
import projects from './aktivbo.json'; // Example JSON file

const items = ref(projects);
const selectedItem = ref(null);

// Handle showing details when a "Details" button is clicked
const handleShowDetails = (item) => {
  selectedItem.value = item;
};
</script>
