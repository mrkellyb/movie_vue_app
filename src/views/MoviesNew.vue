<template>
  <div class="movies-new">
    <h1>Movie Vue App: Add a Movie</h1>

    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
      Title: <input type="text" v-model="newMovieTitle"><br>
      Year: <input type="text" v-model="newMovieYear"><br>
      Plot: <input type="text" v-model="newMoviePlot"><br>
      Director: <input type="text" v-model="newMovieDirector"><br>
      <p><button type="submit">Add New Movie</button></p>
    </form>

  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector
      };
      axios.post("/api/movies", params).then(response => {
        this.$router.push("/movies");
      }).catch(error => {
        this.errors =  error.response.data.errors;
      });
    }
  }
};



</script>