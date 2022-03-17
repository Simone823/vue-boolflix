<template>
    
    <!-- Wrapper -->
    <div class="wrapper">

        <!-- Wrapper movie -->
        <div class="wrapper_movie">
            <div class="categoria" v-if="moviesArray.length > 0">
                <h1>Movies</h1>
            </div>

            <!-- Movie card -->
            <div class="movie_card" v-for="element in moviesArray" :key="element.id">
                <!-- Img wrapper -->
                <div class="img_wrapper">
                    <img :src="`https://image.tmdb.org/t/p/w342/${element.poster_path}`"  alt="">
                </div>

                <!-- Info wrapper -->
                <div class="info_wrapper">
                    <h1 class="title">{{element.title}}</h1>
                    <p class="original_title">{{element.original_title}}</p>

                    <!-- ------------------------------------------------------------------------------------------------------ -->
                    <p class="language" v-if="element.original_language == 'en'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1ec-1f1e7.png" alt="">
                    </p>
                    <p class="language" v-else-if="element.original_language == 'fr'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1eb-1f1f7.png" alt="">
                    </p>
                    <p class="language" v-else-if="element.original_language == 'it'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1ee-1f1f9.png" alt="">
                    </p>
                    <p class="language" v-else>
                        {{element.original_language}}
                    </p>
                    <!-- ------------------------------------------------------------------------------------------------------ -->

                    <span class="vote" v-for="(el, index) in 5" :key="index" :class="index < arrotondoVote(element) ? 'color-yellow' : ''">&starf;</span>
                    <p class="overview">{{element.overview}}</p>
                </div>
            </div>
        </div>

        <!-- Serie tv wrapper -->
        <div class="wrapper_tv">
            <div class="categoria" v-if="tvArray.length > 0">
                <h1>Series Tv</h1>
            </div>

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
                    
                    <!-- ------------------------------------------------------------------------------------------------------ -->
                    <p class="language" v-if="element.original_language == 'en'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1ec-1f1e7.png" alt="">
                    </p>
                    <p class="language" v-else-if="element.original_language == 'fr'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1eb-1f1f7.png" alt="">
                    </p>
                    <p class="language" v-else-if="element.original_language == 'it'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1ee-1f1f9.png" alt="">
                    </p>
                    <p class="language" v-else>
                        {{element.original_language}}
                    </p>
                    <!-- ------------------------------------------------------------------------------------------------------ -->

                    <span class="vote" v-for="(el, index) in 5" :key="index" :class="index < arrotondoVote(element) ? 'color-yellow' : ''">&starf;</span>
                    <p class="overview">{{element.overview}}</p>
                </div>
            </div>

        </div>

        <!-- Loading -->
        <div class="loading" :class="moviesArray.length == 0 && tvArray.length == 0 ? 'active' : '' ">
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
    },

    methods: {

        // Arrotondo numero vote
        arrotondoVote: function(element) {
            return Math.ceil(element.vote_average / 2);
        },
        
    },
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

    .wrapper_movie,
    .wrapper_tv {
        display: flex;
        flex-wrap: wrap;
        gap: 35px;
        row-gap: 35px;

        .categoria {
            width: 100%;
        }

        .movie_card,
        .tv_card {
            width: calc(100% / 6 - 35px);
            position: relative;
            filter: drop-shadow(0 0 5px $color-gray-light);
            min-height: 400px;

            &:hover {
                transform: scale(0.94);
                transition: all 200ms linear;
            }

            &:hover .info_wrapper {
                background-color: rgba($color: $color-black-dark, $alpha: 0.85);
                animation: height 300ms linear;
                opacity: 1;
                transition: opacity 300ms linear;

                @keyframes height {
                    from {
                        height: 0;
                    }

                    100% {
                        height: 100%;
                    }
                }
            }

            .img_wrapper {
                width: 100%;
                height: 100%;

                img {
                    object-fit: cover;
                    object-position: center top;
                }
            }

            .info_wrapper {
                padding: 10px 10px;
                position: absolute;
                top: 0;
                left: 0;
                right: 0;
                bottom: 0;
                overflow-y: auto;
                opacity: 0;

                .title,
                .name {
                    font-size: 18px;
                    text-shadow: $text-shadow-black;
                    margin-bottom: 5px;
                }

                .original_title,
                .original_name {
                    color: $color-green;
                    text-shadow: $text-shadow-black;
                    margin-bottom: 5px;
                }

                .language {
                    margin-bottom: 5px;
                    font-size: 18px;
                    filter: drop-shadow($text-shadow-black);

                    img {
                        width: 22px;
                        height: 22px;
                    }
                }

                .vote {
                    font-size: 20px;
                    filter: drop-shadow($text-shadow-black);

                    &.color-yellow {
                        color: $color-yellow;
                    }
                }

                .overview {
                    margin-top: 5px;
                    text-shadow: $text-shadow-black;
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

    @media screen and (max-width: 1410px) {
        .movie_card,
        .tv_card {
            width: calc(100% / 4 - 35px)!important;
            transition: all 200ms linear;
        }
    }

    @media screen and (max-width: 990px) {
        .movie_card, 
        .tv_card {
            width: calc(100% / 3 - 35px)!important;
            transition: all 200ms linear;
        }
    }

    @media screen and (max-width: 768px) {
        .movie_card,
        .tv_card {
            width: calc(100% / 2 - 35px)!important;
            transition: all 200ms linear;
        }
    }

    @media screen and (max-width: 560px) {
        .movie_card,
        .tv_card {
            width: calc(100% / 1 - 35px)!important;
            transition: all 200ms linear;
            flex-grow: 1;
        }
    }
}


</style>