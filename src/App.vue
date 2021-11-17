<template>
  <div id="app">
      <input v-model="filmToSearch" type="text" id="search" v-on:keyup.enter="onClick()"> 
      <input type="button" value="Cerca" @click="onClick()">
      <h1>Film</h1>
      <ul>
        <li v-for="film in moviesArray" :key="film.id">
          {{film.title}} <br>
          {{film.original_title}} <br>
          <img :src="require(`../src/assets/${getFlag(film.original_language)}`)" alt="" /><br>
          {{film.vote_average}}
        </li>
      </ul>
      <h1>Serie</h1>
      <ul>
        <li v-for="serie in seriesArray" :key="serie.id">
          {{serie.name}} <br>
          {{serie.original_name}} <br>
          <img :src="require(`../src/assets/${getFlag(serie.original_language)}`)" alt="" /><br>
          {{serie.vote_average}}
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
      seriesArray:[],
      filmToSearch:"",
      flagLang: {
        it:"it.svg",
        de:"de.svg",
        fr:"fr.svg",
        jp:"jp.svg",
        en:"gb.svg",
        eu:"eu.svg",
      }
    };
  },
  methods: {
    getFilmOrSeries(url, listArray) {
      axios.get(this.apiUrl + url, {
        params: {
          api_key: this.apiKey,
          query: this.filmToSearch,
        },
        }) .then((resp) => {
          this[listArray] = resp.data.results;
        })
    },
    onClick(){
      this.getFilmOrSeries("/search/movie", "moviesArray");
      this.getFilmOrSeries("/search/tv", "seriesArray");
    },
    getFlag(language) {

      console.log(language)
      if(!this.flagLang[language]) {
        language = "eu";
        console.log(language)
      } else {

        return this.flagLang[language]
      }
      return this.flagLang[language]
    }
  },
};
</script>

<style lang="scss">
img{
  width: 50px;
  height: 20px;
}
</style>
