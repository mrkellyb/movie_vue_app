<template>
  <div class="home">
    <h1>Movie Vue App Actors Index</h1>

    <div>
      <b>Create a New Actor</b><br>
      First Name: <input type="text" v-model="newActorFirstName"><br>
      Last Name: <input type="text" v-model="newActorLastName"><br>
      Known For: <input type="text" v-model="newActorKnownFor"><br>
      Gender: <input type="text" v-model="newActorGender"><br>
      Age: <input type="text" v-model="newActorAge"><br>
      Movie Id: <input type="text" v-model="newMovieId"><br>
      <p><button v-on:click="createActor()">Create New Actor</button></p>
      <hr>

    </div>

    <div v-for="actor in actors">
      <b>{{ actor.first_name }} {{ actor.last_name }}</b><br>
      
<!--       {{ actor.known_for}}<br>
      {{ actor.gender}}<br>
      {{ actor.age}}<br>
      Movie ID: {{ actor.movie_id}}<br>
      Actor ID: {{ actor.id }}<br> -->
      <div>
        <button v-on:click="showActor(actor)">More Info</button>
      </div>
      <div v-if="actor === currentActor">
        Name: {{ currentActor.first_name }} {{ currentActor.last_name }}<br>
        Known For: {{ currentActor.known_for }}<br>
        Gender: {{ currentActor.gender }}<br>
        Age: {{ currentActor.age }}<br>
        Movie ID: {{ currentActor.movie_id }}<br>
        Actor ID: {{ currentActor.actor_id }}
      </div>
      <hr>



    </div>

  </div>
</template>

<style>
</style>

<script>

import axios from "axios";

export default {
  data: function() {
    return {
      actors: [],
    };
  },
  created: function() {
    axios.get("/api/actors").then(response => {
      this.actors = response.data;
    });
  },

  methods: {
    createActor: function() {
      var params = {
        first_name: this.newActorFirstName,
        last_name: this.newActorLastName,
        known_for: this.newActorKnownFor,
        gender: this.newActorGender,
        age: this.newActorAge,
        movie_id: this.newMovieId,
      };

      axios.post("/api/actors", params).then(response => {
        console.log("New Actor Created", response.data);
        this.actors.unshift(response.data);
      });
    },

    showActor: function(actor) {
      if (this.currentActor === actor) {
        this.currentActor = null;
      } else {
        this.currentActor = actor;
      }
    },
    updateActor: function(actor) {
      var params = {
        first_name: actor.first_name,
        last_name: actor.last_name,
        known_for: actor.known_for,
        gender: actor.gender,
        age: actor.age,
        movie_id: actor.movie_id
      };
      axios.patch("/api/actors/" + actor.id, params).then(response => {
        console.log("Actor updated", response.data);
      });
    }
  }
};
</script>