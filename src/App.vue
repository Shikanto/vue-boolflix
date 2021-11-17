<template>
  <div id="app">
      <input v-model="filmToSearch" type="text" id="search" v-on:keyup.enter="getFilm(filmToSearch)"> 
      <input type="button" value="Cerca" @click="getFilm(filmToSearch)">
      <ul>
        <li v-for="(film, i) in moviesArray" :key="i">
          {{film.title}} <br>
          {{film.original_title}} <br>
          {{film.original_language}} <br>
          {{film.vote_average}}
        </li>
      </ul>
  </div>
</template>

<script>
import axios from "axios";


export default {
  name: "App",
  components: {
  },
  data() {
    return {
      apiKey:"444c44e78e3dc1d94571f9837c0e1fc0",
      apiUrl:"https://api.themoviedb.org/3",
      moviesArray:[],
      filmToSearch:"",
    };
  },
  methods: {
    getFilm() {
      axios.get(this.apiUrl + "/search/movie", {
        params: {
          api_key: this.apiKey,
          query: this.filmToSearch,
        },
        }) .then((resp) => {
          this.moviesArray = resp.data.results;
        })
    },
  },
};
</script>

<style lang="scss">

</style>
