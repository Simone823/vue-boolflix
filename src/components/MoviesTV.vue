<template>
    
    <!-- Wrapper -->
    <div class="wrapper">

        <!-- Wrapper movie -->
        <div class="wrapper_movie">

            <!-- Movie card -->
            <div class="movie_card" v-for="element in moviesArray" :key="element.id">
                <!-- Img wrapper -->
                <div class="img_wrapper">
                <img :src="`https://image.tmdb.org/t/p/w342/${element.poster_path}`"  alt="">
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

        <!-- Serie tv wrapper -->
        <div class="tv_wrapper">

            <!-- Tv card -->
            <div class="tv_card" v-for="element in tvArray" :key="element.id">
                <!-- Img wrapper -->
                <div class="img_wrapper">
                    <img :src="`https://image.tmdb.org/t/p/w342/${element.poster_path}`" alt="">
                </div>

                <!-- Info wrapper -->
                <div class="info_wrapper">
                    <h2 class="name">{{element.name}}</h2>
                    <p class="original_name">{{element.original_name}}</p>
                    <p class="original_language">{{element.original_language}}</p>
                    <p class="vote">{{element.vote}}</p>
                </div>
            </div>

        </div>

        <!-- Loading -->
        <div class="loading" :class="moviesArray.length == 0 &&  tvArray.length == 0 ? 'active' : '' ">
            <div class="circle"></div>
            <h2>Nella barra di ricerca scrivi un film o una serie tv e premi invio</h2>
        </div>

    </div>

</template>



<script>
export default {
    name: "MoviesTv",

    props: {
        // arrayMovies
        moviesArray: Array,

        // arrayTv
        tvArray: Array,
    }
}
</script>


<style lang="scss" scoped>
// Import common scss
@import '../assets/scss/common.scss';

.wrapper {
    width: 100%;
    display: flex;
    flex-direction: column;
    row-gap: 80px;

    .wrapper_movie {
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

            .info {
                padding: 0 5px;

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
    }

    .tv_wrapper {
        display: flex;
        flex-wrap: wrap;
        gap: 25px;
        row-gap: 35px;

        .tv_card {
            width: calc(100% / 6 - 25px);

                       .img_wrapper {
                width: 100%;
                height: 380px;
                aspect-ratio: 1/1;
                margin-bottom: 20px;
            }

            .info_wrapper {
                padding: 0 5px;

                .name {
                    font-size: 20px;
                    text-shadow: 0 0 5px black;
                    margin-bottom: 5px;
                }

                .original_name {
                    color: $color-green;
                    text-shadow: 0 0 5px black;
                }

                .original_language {
                    margin-bottom: 8px;
                    font-size: 18px;
                }
            }
        }
    }



    .loading {
        display: none;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateX(-50%) translateY(-50%);

        &.active {
            display: flex;
            flex-direction: column;
        }

        .circle {
            width: 80px;
            height: 80px;
            border: 4px solid $color-red;
            border-top: none;
            border-radius: 50%;
            border-left: none;
            animation: rotate 1.2s linear infinite;
            align-self: center;
            margin-bottom: 25px;
            filter: drop-shadow(0 0 8px $color-red);
        }

        h2 {
            text-shadow: 0 0 5px $color-red;
            font-size: 28px;
        }

        @keyframes rotate {
            from {
                transform: rotate(0deg);
            }

            100% {
                transform: rotate(360deg);
            }
        }
    }
}

</style>