<template>

  <!-- App vue -->
  <div id="app">
    
    <!-- Header -->
    <header>
      <LogoSearch @arrayMovie="recuperoArrayMovie"/>
    </header>

    <!-- Main -->
    <main>
      <MoviesTv :moviesArray="arrayMovieRec"/>
    </main>

  </div>

</template>



<script>
// Import Logo_Search
import LogoSearch from "./components/LogoSearch.vue"

// Import MoviesTv 
import MoviesTv from "./components/MoviesTV.vue"

export default {
  name: 'App',
  components: {
    LogoSearch,
    MoviesTv,
  },

  data() {
    return {

      // recupero Array Movie
      arrayMovieRec: [],

    }
  },

  methods: {

    // Recupero arrayMovie
    recuperoArrayMovie: function(arrayMovie) {
      this.arrayMovieRec = arrayMovie;
    },

  },
}

</script>

<style lang="scss">
// Import common scss
@import './assets/scss/common.scss';

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: "Oregano", cursive;
  letter-spacing: 2px;
  display: flex;
  flex-direction: column;
  height: 100vh;
  
  header {
    padding: 30px;
    background-color: $color-black; 
  }

  main {
    background-color: $color-black-dark; 
    flex-grow: 1;
    color: $color-white;
    overflow-y: auto;
    padding: 20px 20px;
  }
}


</style>
