<template>
  <div class="movies-index">
    <h1>Movie Vue App: Movie Index</h1>

    <div v-for="movie in movies">
      <router-link v-bind:to="'/movies/' + movie.id">
      <b>{{ movie.title }}</b></router-link> ({{ movie.year }})<br>
      <i>{{ movie.plot }}</i><br>
      Directed by {{ movie.director }}<br>
      Movie ID #: {{ movie.id }}
      <hr>
    </div>
    
  </div>
</template>

<script>
  
import axios from "axios";

export default {
  data: function() {
    return {
      movies: [],
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      this.movies = response.data;
    });
  }
};

</script>