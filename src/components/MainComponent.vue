<template>
  <main>
    <div class="container">
      <div class="row">
        <div class="col" v-for="(movie, index) in filterMovies" :key="movie.id">
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
    </div>
  </main>
</template>

<script>
import axios from "axios";
import state from "@/state.js";

export default {
  name: "MainComponent",

  data() {
    return {
      movies: [],
    };
  },
  methods: {
    searchMovie() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=7559f4c99fde3dbacdffc9766ef20e18&language=it-IT&page=1&include_adult=false&query=${state.searchText}`
        )
        .then((response) => {
          console.log(response);
          this.movies = response.data.response;
          state.movies = this.movies;
        })
        .catch((error) => {
          this.error = `${error}`;
        });
    },

    flags(index) {
      if (this.movies[index].original_language === "en") {
        this.movies[index].original_language = "us";
      } else if (this.movies[index].original_language === "ko") {
        this.movies[index].original_language = "kr";
      } else if (this.movies[index].original_language === "da") {
        this.movies[index].original_language = "dk";
      }
      return this.movies[index].original_language;
    },
  },
  computed: {
    filterMovies() {
      this.searchMovie();
      return this.movies.filter((movie) => {
        return movie.title
          .toLowerCase()
          .includes(state.searchText.toLowerCase());
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
