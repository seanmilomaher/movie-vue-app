<template>
  <div class="movies-edit">
    <div>
      <h1>Edit Movie</h1>
      <p>Title: <input type="text" v-model="movie.title"></p>
      <p>Plot: <input type="text" v-model="movie.plot"></p>
      <p>Director: <input type="text" v-model="movie.director"></p>
      <p>Year: <input type="text" v-model="movie.year"></p>
      <button v-on:click="updateMovie">Save Changes</button><br>
      <button v-on:click="destroyMovie">Delete</button>
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
    updateMovie: function() {
      var params = {
        title: this.movie.title,
        plot: this.movie.plot,
        director: this.movie.director,
        year: this.movie.year,  
      };
      axios.patch(`api/movies/${this.movie.id}`, params).then(response => {
        console.log(response.data);
      }).catch(error => {
        console.log(error.response.data.errors)
      });
    },
    destroyMovie: function() {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`api/movies/${this.movie.id}`).then(response => {
          console.log(response.data);
          this.$router.push("/movies");
        })
      }
    }
  }
};
</script>