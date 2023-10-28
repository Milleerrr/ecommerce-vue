<script setup>
import { ref } from 'vue';
import NavBar from './components/NavBar.vue';
import SearchResults from './components/SearchResults.vue';

const currentQuery = ref('');

const updateQuery = (query) => {
  currentQuery.value = query;
};

</script>

<template>
  <div class="mb-5">
    <NavBar @update:query="updateQuery" />
  </div>
  <div>
    <!-- Here, currentQuery is passed as a prop, not as an event -->
    <SearchResults :querySearch="currentQuery" />
  </div>
</template>

<style scoped>
/* ... your styles ... */
</style>
