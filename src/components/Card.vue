<script setup>
import { defineProps, toRefs } from 'vue'

const props = defineProps({
    productInfo: {
        type: Object,
        required: true
    },
})

// Destructure the properties from the productInfo prop for easier access
const { title, description, price, category, thumbnail } = toRefs(props.productInfo)

</script>

<template>
    <div class="card card-item" style="width: 18rem;">
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
            <a href="#" class="card-link">View details</a>
        </div>
    </div>
</template>

<style scoped>
.card-img-top {
    width: 100%;
    height: 15vw;
    object-fit: cover;
}

.card-item {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.5s;
}

.card-item:hover {
    transform: translateY(-10px);
    box-shadow: 0 10px 15px rgba(3, 255, 213, 0.6);
}
</style>
