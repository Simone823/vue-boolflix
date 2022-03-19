<template>

    <!-- Card wrapper-->
    <div class="card_wrapper">
        <!-- Img wrapper -->
        <div class="img_wrapper">
            <img v-if="element.poster_path" :src="`https://image.tmdb.org/t/p/w342/${element.poster_path}`" alt="">
            <img v-else src="../assets/img/cover_default.png" alt="">
        </div>

        <!-- Info wrapper -->
        <div class="info_wrapper">
            <!-- Titolo -->
            <h1 class="title">{{element.title || element.original_name}}</h1>
            <!-- Titolo originale -->
            <p class="original_title">{{element.original_title || element.original_name}}</p>
            <!-- Lingua -->
            <p class="language">
                <img :src="`http://purecatamphetamine.github.io/country-flag-icons/3x2/${flagIcon(element.original_language)}.svg`">
            </p>
            <!-- Voto -->
            <span class="vote" v-for="(el, index) in 5" :key="index" :class="index < arrotondoVote(element) ? 'color-yellow' : ''">&starf;</span>
            <!-- Descrizione -->
            <p class="overview" v-if="element.overview">{{element.overview}}</p>
            <p class="overview" v-else>Descrizione non disponibile</p>
        </div>
    </div>

</template>




<script>
    export default {
        name: "CardItem", 

        props: {

            // Elemento singolo all'interno di arrayMovie e arrayTv
            element: Object,
        },
        
        methods: {

            // Arrotondo numero vote
            arrotondoVote: function(element) {
                return Math.ceil(element.vote_average / 2);
            },

            // Flag icon
            flagIcon: function (unicode) {
                if (unicode == "en") {
                    unicode = "gb";
                }

                // console.log(unicode);
                return unicode.toUpperCase();
            }
        
        },
    }
</script>




<style lang="scss" scoped>
// Import common scss
@import '../assets/scss/common.scss';


.card_wrapper {
    width: calc(100% / 6 - 35px);
    position: relative;
    filter: drop-shadow(0 0 5px $color-gray-light);
    min-height: 400px;
    border-radius: 10px;
    overflow: hidden;

    &:hover {
        transform: scale(0.94);
        transition: all 200ms linear;
    }

    &:hover .info_wrapper {
        background-color: rgba($color: $color-black-dark, $alpha: 0.85);
        animation: height 300ms linear;
        opacity: 1;
        transition: opacity 300ms linear;
        display: block;

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
        display: none;

        .title {
            font-size: 18px;
            text-shadow: $text-shadow-black;
            margin-bottom: 5px;
        }

        .original_title {
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

@media screen and (max-width: 1410px) {
    .card_wrapper {
        width: calc(100% / 4 - 35px)!important;
        transition: all 200ms linear;
    }
}

@media screen and (max-width: 990px) {
    .card_wrapper {
        width: calc(100% / 3 - 35px)!important;
        transition: all 200ms linear;
    }
}

@media screen and (max-width: 768px) {
    .card_wrapper {
        width: calc(100% / 2 - 35px)!important;
        transition: all 200ms linear;
    }
}

@media screen and (max-width: 560px) {
    .card_wrapper {
        width: calc(100% / 1 - 35px)!important;
        transition: all 200ms linear;
        flex-grow: 1;
    }
}

</style>