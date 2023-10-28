<script setup>
import { defineProps, toRefs } from 'vue'

const props = defineProps({
    productInfo: {
        type: Object,
        required: true
    }
})

// Destructure the properties from the productInfo prop for easier access
const { title, description, price, category, thumbnail } = toRefs(props.productInfo)
</script>

<template>
    <div class="card" style="width: 18rem;">
        <!-- Use the thumbnail as the image source -->
        <img :src="thumbnail" class="card-img-top" alt="Product Image">
        <div class="card-body">
            <h5 class="card-title">{{ title }}</h5>
            <p class="card-text">{{ description }}</p>
        </div>
        <ul class="list-group list-group-flush">
            <li class="list-group-item">Price: £{{ price }}</li>
            <li class="list-group-item">Category: {{ category }}</li>
        </ul>
        <div class="card-body">
            <a href="#" class="card-link">Card link</a>
            <a href="#" class="card-link">Another link</a>
        </div>
    </div>
</template>

<style scoped>
    .card-img-top {
        width: 100%;
        height: 15vw;
        object-fit: cover;
    }
</style>
