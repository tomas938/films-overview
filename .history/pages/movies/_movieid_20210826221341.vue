<template>
  <Loading v-if="$fetchState.pending"></Loading>
  <div v-else class="contanier single-movie">
    <Nuxt-link class="button" :to="{ name: 'index' }">Back</Nuxt-link>
    <div class="movie-info">
      <div class="movie-img">
        <img :src="" alt="" />
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
