<template>
    
    <!-- Wrapper -->
    <div class="wrapper">

        <!-- Movie card -->
        <div class="movie_card" v-for="element in moviesArray" :key="element.id">

            <!-- Img wrapper -->
            <div class="img_wrapper">
               <img src="https://picsum.photos/200" alt="">
            </div>

            <!-- Info wrapper -->
            <div class="info">
                <h1 class="title">{{element.title}}</h1>
                <p class="original_title">{{element.original_title}}</p>
                <p class="language">{{element.original_language}}</p>
                <p class="vote">{{element.vote_average}}</p>
            </div>

        </div>
        
    </div>

</template>



<script>
export default {
    name: "MoviesTv",

    props: {
        // arrayMovies
        moviesArray: Array,
    }
}
</script>


<style lang="scss" scoped>
// Import common scss
@import '../assets/scss/common.scss';

.wrapper {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    gap: 25px;
    row-gap: 35px;

    .movie_card {
        width: calc(100% / 6 - 25px);

        .img_wrapper {
            width: 100%;
            height: 380px;
            aspect-ratio: 1/1;
            margin-bottom: 20px;
        }

        .title {
            font-size: 20px;
            text-shadow: 0 0 5px black;
            margin-bottom: 5px;
        }

        .original_title {
            color: $color-green;
            text-shadow: 0 0 5px black;
        }

        .language {
            margin-bottom: 8px;
            font-size: 18px;
        }
    }

}


</style>