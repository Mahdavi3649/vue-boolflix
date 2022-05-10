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
          <div class="col-4" v-for="(movie, index) in movies" :key="movie.id">
            <div class="card-film">
              <div class="cover-film">
                <h5 v-if="movie.poster_path === null">
                  <strong>Titolo:</strong>{{ movie.title }}
                </h5>
                <img
                  v-else
                  :src="'http://image.tmdb.org/t/p/w200/' + movie.poster_path"
                  :alt="movie.title"
                />
              </div>

              <div class="description">
                <p><strong class="gold">Titolo:</strong> {{ movie.title }}</p>
                <p>
                  <strong class="gold">Titolo Originale:</strong>
                  {{ movie.original_title }}
                </p>
                <img
                  :src="'https://flagcdn.com/w20/' + flags(index) + '.png'"
                  alt=""
                />
                <p>
                  <strong class="gold">Voto: </strong>{{ movie.vote_average }}
                </p>
                <p>
                  <strong class="gold">Overview:</strong> {{ movie.overview }}
                </p>
              </div>
            </div>
          </div>
        </div>

        <div class="row">
          <div class="col-4" v-for="(serie, index) in series" :key="serie.id">
            <div class="card-film">
              <div class="cover-film">
                <h5 v-if="serie.poster_path === null">
                  <strong>Titolo:</strong>{{ serie.name }}
                </h5>
                <img
                  v-else
                  :src="'http://image.tmdb.org/t/p/w200/' + serie.poster_path"
                  :alt="serie.name"
                />
              </div>

              <div class="description">
                <p><strong class="gold">Titolo:</strong> {{ serie.name }}</p>
                <p>
                  <strong class="gold">Titolo Originale:</strong>
                  {{ serie.original_name }}
                </p>
                <img
                  :src="'https://flagcdn.com/w20/' + flags(index) + '.png'"
                  class="mb-13"
                />
                <p>
                  <strong class="gold">Voto: </strong>{{ serie.vote_average }}
                </p>
                <p>
                  <strong class="gold">Overview:</strong> {{ serie.overview }}
                </p>
              </div>
            </div>
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
      series: null,
      movies: null,
    };
  },
  methods: {
    searchMovie() {
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
        })
      );
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
  mouted() {
    this.searchMovie();
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
