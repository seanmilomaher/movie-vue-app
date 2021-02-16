<template>
  <div class="movies-index">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h1>Movies</h1>
      <h1>Title: {{movie.title}}</h1>
      <p>Year: {{movie.year}}</p>
      <p>Director: {{movie.director}}</p>
      <p>Plot: {{movie.plot}}</p>
      <router-link :to="`/movies/${movie.id}`"><button>More Info</button></router-link>
    </div>
  </div>
</template>

<style></style>

<script>

import axios from "axios";

export default {
  data: function() {
    return {
      movies: {},
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      console.log(response.data);
      this.movies = response.data;
    })
  },
  methods: {}
};
</script>