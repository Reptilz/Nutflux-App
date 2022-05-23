<template>
  <div class="home">
    <!-- HERO -->
    <Hero />

    <!-- Movies -->
    <div class="container movie">
      <div id="movie-grid" class="movie-grid">
        <div v-for="(movie, index) in movies" :key="index" class="movie">
          <div class="movie-img">
            <img :src="`https://image.tmdb.org/t/p/${movie.poster_path}`" alt="" />
            <p class="review">{{movie.vote_average}}</p>
            <p class="overview">{{movie.overview}}</p>

            
            <!-- ON EST ACTUELLEMENT ICI -->


          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      movies: [],
    }
  },
  async fetch(){
    await this.getMovies()
  },
  methods: {
   async getMovies(){
     const data = axios.get(
       `https://api.themoviedb.org/3/movie/now_playing?api_key=583a93ce4dd56c8af08dcfe52409369f&language=en-US&page=1`
     );
     const result = await data;
     result.data.results.forEach(movie => {
       this.movies.push(movie);
     });
   },
  },
}
</script>
