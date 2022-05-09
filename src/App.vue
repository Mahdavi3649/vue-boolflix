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
      <div class="container">
        <div class="row">
          <div class="col" v-for="(movie, index) in movies" :key="movie.id">
            <img
              :src="'http://image.tmdb.org/t/p/w200/' + movie.poster_path"
              alt=""
            />

            <h3>{{ movie.title }}</h3>
            <p>{{ movie.original_title }}</p>
            <img
              :src="'https://flagcdn.com/w20/' + flags(index) + '.png'"
              alt=""
            />
            <p>{{ movie.vote_average }}</p>
          </div>
        </div>

        <div class="row">
          <div class="col" v-for="(serie, index) in series" :key="serie.id">
            <img
              :src="'http://image.tmdb.org/t/p/w200/' + serie.poster_path"
              alt=""
            />

            <h3>{{ serie.name }}</h3>
            <p>{{ serie.original_name }}</p>
            <img
              :src="'https://flagcdn.com/w20/' + flags(index) + '.png'"
              alt=""
            />
            <p>{{ serie.vote_average }}</p>
          </div>
        </div>
      </div>
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
      series: null,
    };
  },
  methods: {
    searchMovie() {
      let APImovies = axios.get(
        "https://api.themoviedb.org/3/search/movie?api_key=7559f4c99fde3dbacdffc9766ef20e18&language=it-IT&page=1&include_adult=false&query=funny games"
      );
      let APIseries = axios.get(
        "https://api.themoviedb.org/3/search/tv?api_key=7559f4c99fde3dbacdffc9766ef20e18&language=en-US&page=1&include_adult=false&query=black mirror"
      );
      axios.all([APImovies, APIseries]).then(
        axios.spread((...responses) => {
          this.movies = responses[0].data.results;
          this.series = responses[1].data.results;
          this.searchText = "";
        })
      );
    },

    flags(index) {
      if (this.movies[index].original_language === "en") {
        this.movies[index].original_language = "us";
      } else if (this.movies[index].original_language === "de") {
        this.movies[index].original_language = "de";
      }
      return this.movies[index].original_language;
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
