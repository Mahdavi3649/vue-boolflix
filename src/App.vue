<template>
  <div id="app">
    <HeaderComponent />
    <main>
      <div class="container">
        <div class="row">
          <div class="col-4" v-for="(movie, index) in movies" :key="movie.id">
            <div class="card-film">
              <div class="cover-film">
                <h5 v-if="movie.poster_path === null">
                  <strong class="fs-6">Titolo:</strong>{{ movie.title }}
                </h5>
                <img
                  v-else
                  :src="'http://image.tmdb.org/t/p/w200/' + movie.poster_path"
                  :alt="movie.title"
                />
              </div>

              <div class="description">
                <p><strong class="fs-6">Titolo:</strong> {{ movie.title }}</p>
                <p>
                  <strong class="fs-6">Titolo Originale:</strong>
                  {{ movie.original_title }}
                </p>
                <strong class="fs-6">Lingua: </strong>
                <img
                  :src="'https://flagcdn.com/w20/' + flags(index) + '.png'"
                  alt=""
                />
                <p>
                  <strong class="fs-6">Voto: </strong>

                  <font-awesome-icon
                    v-for="n in rating(index)"
                    :key="n"
                    icon="fa-solid fa-star"
                    style="color: gold"
                  />
                  <font-awesome-icon
                    v-for="number in Stars - rating(index)"
                    :key="'r' + number"
                    icon="fa-regular fa-star"
                    style="color: gold"
                  />
                </p>
                <p>
                  <strong class="fs-6">Overview:</strong> {{ movie.overview }}
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
                  <strong class="fs-6">Titolo:</strong>{{ serie.name }}
                </h5>
                <img
                  v-else
                  :src="'http://image.tmdb.org/t/p/w200/' + serie.poster_path"
                  :alt="serie.name"
                />
              </div>

              <div class="description">
                <p><strong class="fs-6">Titolo:</strong> {{ serie.name }}</p>
                <p>
                  <strong class="fs-6">Titolo Originale:</strong>
                  {{ serie.original_name }}
                </p>
                <strong class="fs-6 mb-13">Lingua: </strong>
                <img
                  :src="'https://flagcdn.com/w20/' + flags(index) + '.png'"
                />
                <p>
                  <strong class="fs-6">Voto: </strong>

                  <font-awesome-icon
                    v-for="n in rating(index)"
                    :key="n"
                    icon="fa-solid fa-star"
                    style="color: gold"
                  />
                  <font-awesome-icon
                    v-for="number in Stars - rating(index)"
                    :key="'r' + number"
                    icon="fa-regular fa-star"
                    style="color: gold"
                  />
                </p>
                <p>
                  <strong class="fs-6">Overview:</strong> {{ serie.overview }}
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
import HeaderComponent from "@/components/HeaderComponent.vue";
export default {
  name: "App",
  components: {
    HeaderComponent,
  },

  data() {
    return {
      series: null,
      movies: null,
      Stars: 5,
    };
  },
  methods: {
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

    //  function divided by total vote / 2
    rating(index) {
      return Math.ceil(this.movies[index].vote_average / 2);
    },
  },
  mounted() {
    this.searchMovie();
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
