<template>
  <Loading v-if="$fetchState.pending"></Loading>
  <div v-else class="contanier single-movie">
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
        <div class="movie-fact">
          <span>Revenue:</span>
          {{
            (movie.revenue.toLocaleString('en-us'),
            {
              style: 'currency',
            })
          }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Loading from '../../components/Loading.vue'
export default {
  components: { Loading },
  name: 'single-movie',
  data() {
    return {
      movie: null,
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
    },
  },
}
</script>

<style lang="scss" scoped></style>
