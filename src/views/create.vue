<template>
  <div class="home"> 

    <h1>New Movie</h1>
    <div>
      Title: <input type="text" v-model="newMovieTitle"><br>
      Year: <input type="number" v-model="newMovieYear"><br>
      Plot: <input type="text" v-model="newMoviePlot"><br>
      Director: <input type="text" v-model="newMovieDirector"><br>
      English: <input type="text" v-model="newMovieEnglish"><br>
    </div>
    <br>
    <button v-on:click="createMovie()">Create Movie</button> <br>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      Movies: [],
      currentMovie: {},
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: ""
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      this.movies = response.data;
    });
  },
  methods: {
    createMovies: function() {
      var params = {
        Title: this.newMovieTitle,
        Year: this.newMovieYear,
        Plot: this.newMoviePlot,
        Director: this.newMovieDirector
        English: this.newMovieEnglish
      };
      axios.post("/api/movies", params).then(response => {
        console.log("Success!", response.data);
        this.movies.push(response.data);
        this.newMovieTitle = "";
        this.newMovieYear = "";
        this.newMoviePlot = "";
        this.newMovieDirector = "";
        this.newMovieEnglish = "";
      });
    }
  }

};
</script>