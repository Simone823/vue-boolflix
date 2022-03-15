<template>

  <!-- App vue -->
  <div id="app">
    
    <!-- Header -->
    <header>
      <LogoSearch @arrayMovie="recuperoArrayMovie"/>
    </header>

  </div>

</template>



<script>
// Import Logo_Search
import LogoSearch from "./components/LogoSearch.vue"

export default {
  name: 'App',
  components: {
    LogoSearch,
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
}

header {
  padding: 30px;
  background-color: $color-black; 
}

</style>
