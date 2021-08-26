<template>
  <div class="contanier single-movie"></div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'single-movie',
  data() {
    return {
      movie: null,
    }
  },
  async fetch() {},
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
