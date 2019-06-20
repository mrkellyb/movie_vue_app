<template>
  <div class="movies-show">
    <h1>Movie Vue App: Show Movie</h1>

    <div>
      <b>{{ movie.title }}</b> ({{ movie.year }})<br>
      <i>{{ movie.plot }}</i><br>
      Directed by {{ movie.director }}<br>
      Movie ID #: {{ movie.id }}<br>
      <button><router-link v-bind:to="'/movies/' + movie.id + '/edit'">Edit</router-link></button>
    </div>
  </div>
</template>

<script>
  
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {}
    };
  },
  created: function() {
    axios.get("/api/movies/" + this.$route.params.id).then(response => {
      this.movie = response.data;
      console.log(this.movie);
    });
  }
};

</script>