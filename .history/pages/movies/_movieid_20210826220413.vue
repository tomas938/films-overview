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
      const data = axios.get('')
    },
  },
}
</script>

<style lang="scss" scoped></style>
