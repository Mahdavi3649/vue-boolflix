<template>
  <div id="app">
    <header>
      <div class="d-flex">
        <img src="@/assets/img/logo2.jpg" />
      </div>

      <form class="d-flex" @submit.prevent="searchMovie">
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
          <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
          Search
        </button>
      </form>
    </header>

    <main>
      <ul>
        <li v-for="movie in movies" :key="movie.id">
          <h3>{{ movie.title }}</h3>
          <p>{{ movie.original_title }}</p>
          <p>{{ movie.original_language }}</p>
          <p>{{ movie.vote_average }}</p>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},

  data() {
    return {
      searchText: "",
      movies: null,
      API_URL:
        "https://api.themoviedb.org/3/search/movie?api_key=7559f4c99fde3dbacdffc9766ef20e18&language=en-IT&page=1&include_adult=false&query=funny games",
    };
  },
  methods: {
    searchMovie() {
      axios.get(this.API_URL).then((response) => {
        console.log(response);
        this.movies = response.data.results;
      });
    },
  },
  mouted() {
    this.searchMovie();
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
