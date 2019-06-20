<template>
  <div class="movies-edit">
    <h1>Movie Vue App: Edit Movie</h1>

    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
      Title: <input type="text" v-model="movie.title"><br>
      Year: <input type="text" v-model="movie.year"><br>
      Plot: <input type="text" v-model="movie.plot"><br>
      Director: <input type="text" v-model="movie.director"><br>
      <p><button type="submit">Update Movie</button></p>
    </form>

  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.movie.title,
        year: this.movie.year,
        plot: this.movie.plot,
        director: this.movie.director
      };
      axios.patch("/api/movies/" + this.movie.id, params).then(response => {
        console.log(response.data);
        this.$router.push("/movies/" + this.movie.id);
      }).catch(error => {
        this.errors =  error.response.data.errors;
      });
    }
  }
};



</script>