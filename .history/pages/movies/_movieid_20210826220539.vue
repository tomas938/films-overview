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
  methods: {
    async getSingleMovie() {
      const data = axios.get(`
https://api.themoviedb.org/3/movie/{movie_id}?api_key=<<api_key>>&language=en-US')
    `),
  },
}
</script>

<style lang="scss" scoped></style>
