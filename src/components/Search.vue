<template>
  <div>
    <input v-model="searchQuery" @keyup.enter="search" />
  </div>
</template>

<script>
import axios from 'axios'

const BASE_URL = `https://www.omdbapi.com/?apikey=${process.env.VUE_APP_OMDB_KEY}`

export default {
  name: 'search',
  data() {
    return {
      searchQuery: ''
    }
  },
  search() {
    axios.get(`${BASE_URL}&s=${this.searchQuery}`).then(response => {
      if (response.status === 200) {
        let data = response.data
        if (data.Response === 'True') {
          return this.$emit('search', data.Search)
        }
      }
    })
  }
}
</script>

<style></style>
