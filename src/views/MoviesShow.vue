<template>
  <div class="movies-show">
    <div>
      <h1>Title: {{movie.title}}</h1>
      <p>Plot: {{movie.plot}}</p>
      <p>Director: {{movie.director}}</p>
      <p>Year: {{movie.year}}</p>
      <router-link :to="`/movies/${movie.id}/edit`"><button>Edit</button></router-link>
    </div>
  </div>
</template>

<style></style>

<script>

import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    })
  },
  methods: {

  }
};
</script>