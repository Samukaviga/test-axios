<template>

    <div v-for="movie in movies" :key="movie.id" class="flex column justify-center mt-5">

        <div class="flex flex-col gap-2">
            <div class="flex border p-2 pl-4 pr-8 rouded">
                <button @click="updateMovie(movie)">
                    <div v-if="movie.completed" class="border rounded-full p-3 mx-2 bg-green-500"> </div>
                    <div v-else class="border rounded-full p-3 mx-2 bg-blue-100"> </div>
                </button>
                {{ movie.title }}
                <button class="ml-4 px-2 rounded bg-red-800 text-sm" @click="deleteMovie(movie.id)">Delete</button>
            </div>



        </div>
    </div>

</template>

<script setup>

import axios from "axios";
import { ref } from "vue";

const movies = ref()

axios.get('movies').then((response) => {

    movies.value = response.data

})


function updateMovie(movie) {

    const data = {
        completed: !movie.completed
    }

    axios.patch(`movies/${movie.id}`, data).then((response) => {

        movie.completed = response.data.completed

    })

}

function deleteMovie(id) {


    axios.delete(`movies/${id}`).then((response) => {

        console.log(response);

    });

}



</script>