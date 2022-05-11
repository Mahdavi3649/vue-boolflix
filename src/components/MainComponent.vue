<template>
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
              <img :src="'https://flagcdn.com/w20/' + flags(index) + '.png'" />
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
</template>

<script>
import state from "@/state.js";

export default {
  name: "MainComponent",

  data() {
    return {
      series: null,
      movies: [],
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
  computed: {
    searchMovies() {
      return state.movies;
    },
  },
};
</script>

<style lang="scss" scoped>
main {
  min-height: calc(100vh - 70px);
  background-color: gray;
  .row {
    padding-top: 3rem;
    row-gap: 3rem;
  }

  .card-film {
    overflow-y: hidden;
    width: 340px;
    height: 460px;
    border: 2px solid white;
    background-color: black;
    h5 {
      color: gold;
      padding: 50px 25px;
    }
    .cover-film {
      img {
        height: 100%;
        width: 100%;
      }
    }
  }

  .description {
    display: none;

    .gold {
      color: gray;
    }
    .mb-13 {
      margin-bottom: 13px;
    }
  }

  .card-film:hover .cover-film {
    display: none;
  }
  .card-film:hover .description {
    display: block;
    background-color: black;
    color: white;
    padding: 50px 25px;
    font-size: 14px;
  }
}
</style>
