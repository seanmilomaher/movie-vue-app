<template>
  <div class="movies-new">
    <div>
      <h1>New Movie</h1>
      <p>
        Title:
        <input type="text" v-model="newMovieTitle" />
      </p>
      <p>
        Plot:
        <input type="text" v-model="newMoviePlot" />
      </p>
      <small v-if="newMoviePlot.length > 10">{{ 400 - newMoviePlot.length }} characters remaining</small>
      <p>
        Director:
        <input type="text" v-model="newMovieDirector" />
      </p>
      <p>
        Year:
        <input type="text" v-model="newMovieYear" />
      </p>
      <button v-on:click="createMovie">Create Movie</button>
      <br />
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      newMovieTitle: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieYear: "",
    };
  },
  created: function() {},
  methods: {
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        year: this.newMovieYear,
      };
      axios
        .post("api/movies", params)
        .then(response => {
          console.log(response.data);
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
