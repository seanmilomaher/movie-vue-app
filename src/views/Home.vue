<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="createMovie">Create Movie</button><br>
    <input type="text" v-model="newMovieTitle"><br>
    <input type="text" v-model="newMoviePlot"><br>
    <input type="text" v-model="newMovieDirector"><br>
    <input type="text" v-model="newMovieYear"><br>
    <input type="text" v-model="newMovieEnglish"><br>
    
    <div v-for="movie in movies" v-bind:key="movie">
      <h1>Title: {{movie.title}}</h1>
      <p>Year: {{movie.year}}</p>
      <p>Director: {{movie.director}}</p>
      <p>Plot: {{movie.plot}}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      movies: [],
      newMovieTitle: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieYear: "",
      newMovieEnglish: "",
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log(response.data);
        this.movies = response.data;
      })
    },
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        year: this.newMovieYear,
        english: this.newMovieEnglish,
      };
      axios.post("api/movies", params).then(response => {
        console.log(response.data);
        this.movies.push(response.data);
      });
    }
  }
};
</script>