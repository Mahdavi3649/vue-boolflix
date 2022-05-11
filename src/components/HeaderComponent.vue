<template>
  <header>
    <div class="logo">
      <img src="@/assets/img/logo2.jpg" />
    </div>

    <searchBox v-model="searchText" @searchMovie="searchMovie" />
  </header>
</template>

<script>
import axios from "axios";
import state from "@/state.js";
import searchBox from "@/components/searchBox.vue";
export default {
  name: "HeaderComponent",
  components: {
    searchBox,
  },

  data() {
    return {
      searchText: "",
      movies: [],
    };
  },

  methods: {
    searchMovie() {
      console.log(this.searchText);

      let APImovies = axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=7559f4c99fde3dbacdffc9766ef20e18&language=it-IT&page=1&include_adult=false&query=${this.searchText}`
      );
      let APIseries = axios.get(
        `https://api.themoviedb.org/3/search/tv?api_key=7559f4c99fde3dbacdffc9766ef20e18&language=en-US&page=1&include_adult=false&query=${this.searchText}`
      );

      axios.all([APImovies, APIseries]).then(
        axios.spread((...responses) => {
          this.movies = [
            ...responses[0].data.results,
            ...responses[1].data.results,
          ];
          this.searchText = "";
          console.log(this.movies);
          state.movies = this.movies;
        })
      );
    },
  },
};
</script>

<style lang="scss" scoped>
header {
  display: flex;
  justify-content: space-between;
  background-color: black;
  height: 70px;
  padding: 1rem;

  img {
    width: 130px;
  }
}
</style>
