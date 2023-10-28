<script setup>
import { ref, onMounted, defineProps, computed } from 'vue';
import Card from './Card.vue';

// Destructure the prop
const { querySearch } = defineProps(['querySearch']);


const products = ref([]);

// Component functions
const getItems = async () => {
    try {
        let response = await fetch('https://dummyjson.com/products?limit=50');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        let data = await response.json();
        products.value = data.products;
    } catch (error) {
        console.error("There was a problem fetching the products:", error);
    }
};

const filteredProducts = computed(() => {
    if (querySearch.value && querySearch.value.trim() !== '') {
        return products.value.filter(product => product.title.toLowerCase().includes(querySearch.value.toLowerCase()));
    } else {
        return products.value;
    }
});




// Run on startup
onMounted(getItems);
</script>

<template>
    <div v-if="products.length" class="container text-center">
        <div class="row">
            <div v-for="product in filteredProducts" :key="product.id" class="col mb-4 d-flex align-items-stretch">
                <Card :product-info="product" />
            </div>
        </div>
    </div>
</template>
