<template>
  <div class="home">
    <Hero></Hero>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      movie: [],
    }
  },
  methods: {
    async getMovies() {
      const data = axios(
        'https://api.themoviedb.org/3/movie/now_playing?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US&page=1'
      )
    },
  },
}
</script>
