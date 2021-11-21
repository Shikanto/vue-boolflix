<template>
  <div class="navbar">
    <h1>BOOLFLIX</h1>
    <div class="navbar-search">
      <h3>Cerca la tua serie o il tuo film preferito:</h3>
      <input
        class="input-search"
        v-model="filmToSearch"
        type="text"
        id="search"
        v-on:keyup.enter="onClick()"
      />
      <input class="btn-search" type="button" value="Cerca" @click="onClick()" />
    </div>
  </div>
</template>
<script>
export default {
  name: "Header",
  data() {
    return {
      filmToSearch: "",
      filmSearched: "",
    };
  },
  methods: {
    onClick() {
      this.filmSearched = this.filmToSearch;
      this.$emit("searchFilmSeries", this.filmSearched);
    },
  },
};
</script>
<style lang="scss" scoped>
h1{
        color: red;
        font-weight: bold;
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        letter-spacing: 3px;
        
    }
</style>
