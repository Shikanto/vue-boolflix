<template>
  <div id="app">
    <Header @searchFilmSeries="click"></Header>
    <div class="container">
      <h1>Film</h1>
      <div class="container-films_series">
        <Card
          v-for="(film, i) in moviesArray"
          :key="i"
          :infoFilm="film"
          :flags="flagLang"
        ></Card>
      </div> 
      <h1>Serie</h1>
      <div class="container-films_series">
        <Card
          v-for="(film, i) in seriesArray"
          :key="i"
          :infoFilm="film"
          :flags="flagLang"
        ></Card>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Card from "./components/Card.vue";

export default {
  name: "App",
  components: { Card, Header },
  data() {
    return {
      apiKey: "444c44e78e3dc1d94571f9837c0e1fc0",
      apiUrl: "https://api.themoviedb.org/3",
      moviesArray: [],
      seriesArray: [],
      filmOrSeriesSearched: "",
      flagLang: {
        it: "it.svg",
        de: "de.svg",
        fr: "fr.svg",
        ja: "jp.svg",
        en: "gb.svg",
        eu: "eu.svg",
      },
    };
  },
  methods: {
    //faccio la chiamata per ottenere un array dei film/serie ricercati
    getFilmOrSeries(url, listArray) {
      axios
        .get(this.apiUrl + url, {
          params: {
            api_key: this.apiKey,
            query: this.filmOrSeriesSearched,
          },
        })
        .then((resp) => {
          this[listArray] = resp.data.results;
        });
    },
    click(filmSearched) {
      //qui vado a prendere il dato passato dal figli Card.vue tramite $emit e lo salvo nei data
      this.filmOrSeriesSearched = filmSearched;
      //e poi eseguo la funzione
      this.getFilmOrSeries("/search/movie", "moviesArray");
      this.getFilmOrSeries("/search/tv", "seriesArray");
    },
  },
};
</script>

<style lang="scss">
@import "style/app.scss";
</style>
