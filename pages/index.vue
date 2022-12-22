<template>
  <div>
    <!-- {{ movies }} -->
    <movieHero />
    <!-- movies section -->
    <div class="movie-container">
      <div id="movie-section" class="movie-grid" />
      <div class="movie" v-for="(movie, index) in movies " :key="index">
         <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`">
    </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data () {
    return {
      movies: []
    }
  },
  async fetch () {
    await this.getMovies()
  },
  methods: {
    async getMovies () {
      const data = axios.get(
        'https://api.themoviedb.org/3/movie/now_playing?api_key=bc02c5e8b01df103a3545056d57e9b59&language=en-US&page=1'
      )
      // https://api.themoviedb.org/3/movie/550?api_key=bc02c5e8b01df103a3545056d57e9b59

      const result = await data
      // console.log(result.data)
      result.data.results.forEach((movie) => {
        this.movies.push(movie)
      })
      console.log(this.movies)
    }
  }
}
</script>
