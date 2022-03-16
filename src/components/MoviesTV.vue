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
                <div class="info">
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
                </div>
            </div>
        </div>

        <!-- Serie tv wrapper -->
        <div class="tv_wrapper">
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
                    <p class="original_language" v-if="element.original_language == 'en'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1ec-1f1e7.png" alt="">
                    </p>
                    <p class="original_language" v-else-if="element.original_language == 'fr'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1eb-1f1f7.png" alt="">
                    </p>
                    <p class="original_language" v-else-if="element.original_language == 'it'">
                        <img src="https://images.emojiterra.com/twitter/v13.1/512px/1f1ee-1f1f9.png" alt="">
                    </p>
                    <p class="original_language" v-else>
                        {{element.original_language}}
                    </p>
                    <!-- ------------------------------------------------------------------------------------------------------ -->

                    <span class="vote" v-for="(el, index) in 5" :key="index" :class="index < arrotondoVote(element) ? 'color-yellow' : ''">&starf;</span>
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

    .wrapper_movie {
        display: flex;
        flex-wrap: wrap;
        gap: 25px;
        row-gap: 35px;

        .categoria {
            width: 100%;
        }

        .movie_card {
            width: calc(100% / 6 - 25px);

            .img_wrapper {
                width: 100%;
                height: 380px;
                aspect-ratio: 1/1;
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
                    margin-bottom: 5px;
                }

                .language {
                    margin-bottom: 8px;
                    font-size: 18px;

                    img {
                        width: 22px;
                        height: 22px;
                    }
                }

                .vote {
                    &.color-yellow {
                        color: yellow;
                    }
                }
            }
        }
    }

    .tv_wrapper {
        display: flex;
        flex-wrap: wrap;
        gap: 25px;
        row-gap: 35px;

        .categoria {
            width: 100%;
        }

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
                    margin-bottom: 5px;
                }

                .original_language {
                    margin-bottom: 8px;
                    font-size: 18px;

                    img {
                        width: 22px;
                        height: 22px;
                    }
                }

                    .vote {
                    &.color-yellow {
                        color: yellow;
                    }
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