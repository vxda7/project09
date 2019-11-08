<template>
  <div id="app">
    <div class="container">
      <!-- 1-3. 호출하시오. 
        필요한 경우 props를 데이터를 보내줍니다.
      -->
      <MovieList v-bind:movieDataFromApp="movieData" v-bind:genreDataFromApp="genreData"/>
    </div>
  </div>
</template>

<script>
// const axios = require('axios');
// 1-1. 저장되어 있는 MovieList 컴포넌트를 불러오고,
import MovieList from './components/movies/MovieList'
import axios from 'axios'

export default {
  name: 'app',
  // 1-2. 아래에 등록 후
  components: {
    MovieList,
  },

  data() {
    return {
      // 활용할 데이터를 정의하시오.
      movieData: [],
      genreData: [],
    }
  },
  mounted() {
    // 0. mounted 되었을 때, 
    // 1) 제시된 URL로 요청을 통해 data의 movies 배열에 해당 하는 데이터를 넣으시오. 
    // 2) 제시된 URL로 요청을 통해 data의 genres 배열에 해당 하는 데이터를 넣으시오.
    // axios는 위에 호출되어 있으며, node 설치도 완료되어 있습니다.
    const MOVIE_URL = 'https://gist.githubusercontent.com/sy7979/5d2edfa3f0d0d598906a4e1255f58006/raw/1335851eb414504aca30f1cdab58148f505e0d94/movie.json'
    axios.get(MOVIE_URL)
      .then((response) => {
        
        this.movieData = response.data
      })
      .catch((error) => {
        console.log(error)
      })
  
    const GENRE_URL = 'https://gist.githubusercontent.com/sy7979/ddd308f553f9c6d959e730ff98a7f431/raw/2a6aabc6ae7d378e237df44b3784e971bb09e682/genre.json'
    axios.get(GENRE_URL)
      .then((response) => {
      
        this.genreData = response.data
      })
      .catch((error) => {
        console.log(error)
      })
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
