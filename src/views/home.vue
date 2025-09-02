<template>

    <div v-for="movie in movies" :key="movie.id" class="flex column justify-center mt-5">
        <p>{{ movie.title }}</p>
    </div>

</template>

<script setup>

import axios from "axios";
import { ref } from "vue";

const movies = ref()

axios.get('movies').then((response) => {
    //  console.log(response.data) 

    movies.value = response.data

})


</script>