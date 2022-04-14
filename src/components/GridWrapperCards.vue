<template>
    
    <!-- Wrapper -->
    <div class="grid_wrapper">

        <!-- Categoria movies -->
        <div class="categoria" v-if="moviesArray.length > 0">
            <h1>Film</h1>
        </div>
        <CardItem v-for="element in moviesArray" :key="element.id" :element="element"/>

        <!-- Categoria serie tv -->
        <div class="categoria" v-if="tvArray.length > 0">
            <h1 class="series_tv">Serie Tv</h1>
        </div>
        <CardItem v-for="element in tvArray" :key="element.id" :element="element"/>

        <!-- Categoria film popolari -->
        <div class="categoria" v-if="moviePopularArray.length > 0">
            <h1 class="popular">Film Popolari</h1>
        </div>
        <CardItem v-for="element in moviePopularArray" :key="element.id" :element="element"/>

        <!-- Categoria serie tv popolari -->
        <div class="categoria" v-if="tvPopularArray.length > 0">
            <h1 class="popular">Serie Tv Popolari</h1>
        </div>
        <CardItem v-for="element in tvPopularArray" :key="element.id" :element="element"/>

    </div>

</template>



<script>
// Import CadItem
import CardItem from "./CardItem.vue"

export default {
    name: "GridWrapperCards",

    components: {
        CardItem,
    },

    props: {
        // arrayMovies componente app
        moviesArray: Array,

        // arrayTv componente app
        tvArray: Array,

        // arrayMoviePopular app
        moviePopularArray: Array,

        // arrayTvPopular
        tvPopularArray: Array,
    },

}
</script>


<style lang="scss" scoped>
// Import common scss
@import '../assets/scss/common.scss';

.grid_wrapper {
    width: 100%;
    display: flex;
    row-gap: 80px;
    flex-wrap: wrap;
    gap: 35px;

    .categoria {
        width: 100%;
        text-shadow: 0 0 5px $color-red;

        .series_tv {
            margin-top: 50px;
        }
    }
}
</style>