<template>

  <!-- App vue -->
  <div id="app">
    
    <!-- Header -->
    <header>
      <LogoSearch @arrayMovie="recuperoArrayMovie" @arrayTv="recuperoArrayTv" @arrayMoviePopular="recuperoArrayMoviePop" @arrayTvPopular="recuperoArrayTvPop"/>
    </header>

    <!-- Main -->
    <main>
      <GridWrapperCards :moviesArray="arrayMovieRec" :tvArray="arrayTvRec" :moviePopularArray="arrayMoviePopRec" :tvPopularArray="arrayTvPopRec"/>
      <LoadingCircle class="loader" :class="arrayMovieRec.length == 0 && arrayTvRec.length == 0 && arrayMoviePopRec.length == 0 && arrayTvPopRec.length == 0 ? 'active' : ''"/>
    </main>

  </div>

</template>



<script>
// Import Logo_Search
import LogoSearch from "./components/LogoSearch.vue";

// Import GridWrapperCards
import GridWrapperCards from "./components/GridWrapperCards.vue";

// Import LoadingCircle
import LoadingCircle from"./components/LoadingCircle.vue"

export default {
  name: 'App',
  components: {
    LogoSearch,
    GridWrapperCards,
    LoadingCircle,
  },

  data() {
    return {

      // recupero Array Movie
      arrayMovieRec: [],

      // recupero array tv
      arrayTvRec: [],

      // recupero arrayMoviePopular
      arrayMoviePopRec: [],

      // recupero arrayTvPopular
      arrayTvPopRec: [],

    }
  },

  methods: {

    // Recupero arrayMovie
    recuperoArrayMovie: function(arrayMovie) {
      this.arrayMovieRec = arrayMovie;
    },

    // Recupero array Tv
    recuperoArrayTv: function(arrayTv) {
      this.arrayTvRec = arrayTv;
    },

    // Recupero arrayMoviePopular
    recuperoArrayMoviePop: function(arrayMoviePopular) {
      this.arrayMoviePopRec = arrayMoviePopular;
    },

    // Recupero arrayMoviePopular
    recuperoArrayTvPop: function(arrayTvPopular) {
      this.arrayTvPopRec = arrayTvPopular;
    }

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
    position: relative;

    .loader{
      display: none;

      &.active {
        display: flex;
      }
    }
  }
}


</style>
