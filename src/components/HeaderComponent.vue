<template>
  <header>
    <div class="logo">
      <img src="@/assets/img/logo2.jpg" />
    </div>

    <form
      class="d-flex"
      @submit.prevent="searchMovie"
      @searchMovie="searchMovie"
      :searchText="searchText"
    >
      <input
        class="form-control me-2"
        type="search"
        placeholder="Search"
        aria-label="Search"
        v-model="searchText"
      />
      <button
        class="btn btn-outline-danger d-flex align-items-center"
        type="submit"
      >
        Search
      </button>
    </form>
  </header>
</template>

<script>
import axios from "axios";
import state from "@/state.js";
export default {
  name: "HeaderComponent",

  data() {
    return {
      searchText: "",
    };
  },

  methods: {
    searchMovie(array) {
      let APImovies = axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=7559f4c99fde3dbacdffc9766ef20e18&language=it-IT&page=1&include_adult=false&query=${this.searchText}`
      );
      let APIseries = axios.get(
        `https://api.themoviedb.org/3/search/tv?api_key=7559f4c99fde3dbacdffc9766ef20e18&language=en-US&page=1&include_adult=false&query=${this.searchText}`
      );

      axios.all([APImovies, APIseries]).then(
        axios.spread((...responses) => {
          this.array = [
            ...responses[0].data.results,
            ...responses[1].data.results,
          ];
          state.movies = array;
          this.searchText = "";
        })
      );
    },
  },
  mounted() {
    this.searchMovie();
  },
};
</script>

<style lang="scss" scoped></style>
