<script setup>
import { ref, onMounted, defineProps, toRefs, computed } from 'vue';
import Card from './Card.vue';

// Defining props
const props = defineProps({
    querySearch: String
});

// Making props reactive
const { querySearch } = toRefs(props);

// Declaring Variables
const products = ref([]);
let selectedItem = ref(null);

// Functions
const filteredProducts = computed(() => {
    if (querySearch.value && querySearch.value.trim() !== '') {
        return products.value.filter(product => product.title.toLowerCase().includes(querySearch.value.toLowerCase()));
    } else {
        return products.value;
    }
});

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

const updateSelectedItem = (clickedProduct) => {
    selectedItem.value = clickedProduct;
    console.log('Item selected displayed');
}

onMounted(getItems);

</script>

<template>
    <div class="container text-center">
        <div class="row">
            <div v-if="!selectedItem" v-for="product in filteredProducts" :key="product.id"
                class="col mb-4 d-flex align-items-stretch">
                <Card :product-info="product" @updatedSelectedItem="updateSelectedItem" />
            </div>
            <div v-else>
                <div class="mb-4" @click="selectedItem = null">
                    <button class="btn btn-primary" id="show-all" type="button">Go back</button>
                </div>
                <div class="col mb-4 d-flex align-items-stretch">
                    <Card :product-info="selectedItem" />
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
#show-all {
    display: flex;
    justify-content: start;
}

#show-all:hover {
    color: #003cff;
    background-color: white;
}
</style>