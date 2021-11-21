<template>
<div class="container-card">
    <div class="card">
        <img class="poster-film" :src="`${urlImg}${dimImg}${getPathImg()}`" alt="" />
        <div class="card-body">
            <h2>Titolo: </h2><span class="text-underline">{{ infoFilm.title }}{{infoFilm.name}}</span> <br>
            <h2>Titolo Originale: </h2><span class="text-underline">{{ infoFilm.original_title }}{{infoFilm.original_name}}</span> <br>
            <h2>Lingua Originale: </h2>
                <img
                class="flag"
                :src="require(`../assets/${getFlag(infoFilm.original_language)}`)"
                alt=""
                />
            <div>
                <h2>Voto Film:</h2>
                <!-- inserisco prima le stelline piene in base al voto -->
                <i 
                v-for="(fullStar, i) in getStars(infoFilm.vote_average)"
                :key="'fullStar' + i"
                class="fa fa-star yellow"
                aria-hidden="true"
                ></i>
                <!-- aggiungo le stelline vuote su una base di 5 sottraendo le stelline piene -->
                <i
                v-for="(emptyStar, i) in 5 - getStars(infoFilm.vote_average)"
                :key="'emptyStar' + i"
                class="fa fa-star-o white"
                aria-hidden="true"
                ></i>
            </div>
            <div class="text-centre">
                <h2>Trama</h2>
                <p class="overview">{{infoFilm.overview}}</p>
            </div>
        </div>
    </div>
</div>
</template>
<script>
export default {
  name: "Card",
  data() {
    return {
      urlImg: "https://image.tmdb.org/t/p/",
      dimImg: "w342",
      placeholderFilm: require("../assets/film-poster-placeholder.png"),
    };
  },
  props: {
    infoFilm: Object,
    flags: Object,
  },
  methods: {
    getFlag(language) {
      //console.log(language)
      //se la flag non c'è nel mio array di bandiere metto di default quella europea
      if (!this.flags[language]) {
        language = "eu";
        //console.log(language)
      } else {
        return this.flags[language];
      }
      return this.flags[language];
    },
    getPathImg() {
      //creo una variabile dove salvare l'immagine del poster

      let pathImg = this.infoFilm.poster_path;
      // se non c'è l'immagine resetto e metto un placeholder
      if (!pathImg) {
        pathImg = this.placeholderFilm;
        this.urlImg = "";
        this.dimImg = "";
      } else {
        return pathImg;
      }

      return pathImg;
    },
    getStars(voteNumber) {
      // creo una variabile per salvare il voto
      let voteStar = 0;
      // arrotondo il voto per trasformarlo in voto fino a 5
      voteStar = Math.round(voteNumber / 2);
      console.log(voteStar);
      return voteStar;
    },
  },
};
</script>
<style lang="scss" scoped>

</style>