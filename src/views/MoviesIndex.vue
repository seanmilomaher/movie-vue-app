<template>
  <div class="movies-index">
    <div>
      <h1>Movies</h1>
      Search by name:
      <input v-model="titleFilter" list="titles" />
      <datalist id="titles">
        <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
      </datalist>
      <br />
      <button v-on:click="sortAttribute = 'title'">Sort Alphabetically</button>
      <button v-on:click="sortAttribute = 'plot'">Sort by Plot</button>
      <button v-on:click="sortAttribute = 'director'">Sort by Director</button>
      <button v-on:click="sortAttribute = 'year'">Sort by Year</button>
    </div>
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute)" v-bind:key="movie.id">
      <h1>Title: {{ movie.title }}</h1>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}`"><button>More Info</button></router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],

  data: function() {
    return {
      movies: {},
      titleFilter: "",
      sortAttribute: "",
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
