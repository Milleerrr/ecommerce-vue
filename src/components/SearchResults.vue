<script setup>
import { ref, onMounted, defineProps, toRefs} from 'vue'
import Card from './Card.vue';

const products = ref([]);

defineProps({
    querySearch: String
})

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
}

const filteredProducts = () => {
    return querySearch
        ? sortedProducts.filter(
            product => product.title.toLowerCase().indexOf(querySearch.toLowerCase()) != -1
        )
        : sortedProducts;
}

const sortedProducts = () => {
    return products.value.sort((productA, productB) => {

        const propA = getProductPropForSorting(productA);
        const propB = getProductPropForSorting(productB);

        if (propA < propB)
            return -1;
        if (propB < propB)
            return 1;

        return 0;
    });
}

// Run on start up
onMounted(getItems);


</script>

<template>
    <div v-if="products.length" class="container text-center">
        <div class="row">
            <div v-for="product in products" :key="product.id" class="col mb-4 d-flex align-items-stretch">
                <Card :product-info="product"/>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
