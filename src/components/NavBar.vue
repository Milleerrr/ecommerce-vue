<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['update:query']);

const emitQuery = () => {
    emit('update:query', query);
}

// Vairables 
let query = '';

</script>

<template>
    <nav class="navbar navbar-expand-lg bg-body-tertiary container mt-4 mb-5">
        <div class="container-fluid">
            <a class="navbar-brand hover" href="#">Ecommerce</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
                aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item">
                        <a class="nav-link hover" aria-current="page" href="#">About</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link hover" href="#">Pricing</a>
                    </li>
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle hover" href="#" role="button" data-bs-toggle="dropdown"
                            aria-expanded="false">
                            Filter
                        </a>
                        <ul class="dropdown-menu">
                            <li><a class="dropdown-item hover" href="#">Title</a></li>
                            <li><a class="dropdown-item hover" href="#">Price</a></li>
                            <li><a class="dropdown-item hover" href="#">Category</a></li>
                        </ul>
                    </li>
                </ul>
                <form class="d-flex" role="search">
                    <input v-model="query" @input="emitQuery" class="form-control me-2" type="search" placeholder="Search"
                        aria-label="Search">
                    <button class="btn btn-outline-success" @click.prevent type="submit">Search</button>
                </form>
            </div>
        </div>
    </nav>
</template>

<style scoped>
.hover:hover {
    color: #003cff;
    text-shadow: 0px 5px 30px #034dfa;
    -moz-transition: all 0.2s ease-in;
    -o-transition: all 0.2s ease-in;
    -webkit-transition: all 0.2s ease-in;
    transition: all 0.2s ease-in;
}
</style>
