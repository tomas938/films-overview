<template>
  <Loading v-if="$fetchState.pending"></Loading>
  <transition name="home" v-else>
    <div class="container single-movie">
      <Nuxt-link class="button" :to="{ name: 'index' }">Back</Nuxt-link>
      <div class="movie-info">
        <div class="movie-img">
          <img
            :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
            alt=""
          />
        </div>
        <div class="movie-content">
          <h1>Title: {{ movie.title }}</h1>
          <p class="movie-fact tagline">
            <span>Tagline:</span>"{{ movie.tagline }}"
          </p>
          <p class="movie-fact">
            <span>Released:</span>
            {{
              new Date(movie.release_data).toLocaleString('en-us', {
                month: 'long',
                day: 'numeric',
                year: 'numeric',
              })
            }}
          </p>
          <p class="movie-fact">
            <span>Duration:</span> {{ movie.runtime }} minutes
          </p>
          <p class="movie-fact">
            <span>Budget:</span>
            {{
              movie.budget.toLocaleString('en-us', {
                style: 'currency',
                currency: 'USD',
              })
            }}
          </p>
          <p class="movie-fact">
            <span>Revenue:</span>
            {{
              movie.revenue.toLocaleString('en-us', {
                style: 'currency',
                currency: 'USD',
              })
            }}
          </p>
          <p class="movie-fact"><span>Overview:</span> {{ movie.overview }}</p>
          <p class="movie-fact" v-if="movie.production_companies.length > 0">
            <span>Production companies:</span>
          </p>
          <div
            v-for="(company, index) in movie.production_companies"
            :key="index"
            class="production-company"
          >
            <p v-if="company.logo_path !== null" class="movie-fact">
              {{ company.name }}
            </p>
            <img
              v-if="company.logo_path !== null"
              :src="`https://image.tmdb.org/t/p/w500/${company.logo_path}`"
              alt=""
            />
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import axios from 'axios'
import Loading from '../../components/Loading.vue'
export default {
  transition: 'home',
  components: { Loading },
  name: 'single-movie',
  head() {
    return {
      title: this.movie.title,
    }
  },
  data() {
    return {
      movie: 'null',
    }
  },
  async fetch() {
    await this.getSingleMovie()
  },
  fetchDelay: 1000,
  methods: {
    async getSingleMovie() {
      const data = axios.get(
        `https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=a0b65c5ae8f856e9b3307cd48815620d&language=en-US'`
      )
      const result = await data
      this.movie = result.data
      console.log(result)
    },
  },
}
</script>

<style lang="scss" scoped>
.home-enter-active,
.home-leave-active {
  transition: opacity 0.5s;
}
.home-enter,
.home-leave-active {
  opacity: 0;
}
.single-movie {
  color: #fff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 32px 16px;
  .button {
    align-self: flex-start;
    margin-bottom: 32px;
  }
  .movie-info {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 32px;
    color: #fff;
    @media (min-width: 800px) {
      flex-direction: row;
      align-items: flex-start;
    }
    .movie-img {
      img {
        max-height: 500px;
        width: 100%;
        @media (min-width: 800px) {
          max-height: 700px;
          width: initial;
        }
      }
    }
    .movie-content {
      h1 {
        font-size: 56px;
        font-weight: 400;
      }
      .movie-fact {
        margin-top: 12px;
        font-size: 20px;
        line-height: 1.5;
        span {
          font-weight: 600;
          text-decoration: underline;
        }
      }
      .tagline {
        font-style: italic;
        span {
          font-style: normal;
        }
      }
      .production-company {
        img {
          width: 150px;
          height: 100%;
          object-fit: cover;
        }
      }
    }
  }
}
</style>
