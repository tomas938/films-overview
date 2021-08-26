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
  async fetch() {
    await this.getMovies()
  },
  methods: {
    async getMovies() {
      const data = axios(
        'https://api.themoviedb.org/3/movie/now_playing?api_key=a0b65c5ae8f856e9b3307cd48815620d&language=en-US&page=1'
      )
      const result = await data
      result.data.resu
    },
  },
}
</script>
