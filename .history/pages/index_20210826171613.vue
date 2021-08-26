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
        'https://api.themoviedb.org/3/movie/76341?api_key=a0b65c5ae8f856e9b3307cd48815620d'
      )
    },
  },
}
</script>
