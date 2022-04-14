<template>

    <!-- header Wrapper -->
    <div class="header_wrapper">

        <!-- Logo header -->
        <div class="logo_wrapper">
            <!-- Logo -->
            <img src="../assets/img/netflix_logo.svg" alt="">
        </div>

        <!-- Menu -->
        <ul class="menu">
            <li :class="activeMenu1 == true ? 'active' : '' " @click="getMoviePopular()">Film Popolari</li>
            <li :class="activeMenu2 == true ? 'active' : '' " @click="getTvPopular()">Serie tv Popolari</li>
        </ul>

        <!-- Input text, button -->
        <div class="search_btn_wrapper">
            <!-- Input text -->
            <input type="text" v-model="userInput" @keyup.enter="getServerMovies(), getServerTv()" placeholder="Cerca un film o una serie tv">

            <!-- Button -->
            <button @click="getServerMovies(), getServerTv()">
                <img src="../assets/img/search_logo.png" alt="">
            </button>
        </div>

    </div>

</template>



<script>
// Import axios
import axios from 'axios';

export default {
    name: "LogoSearch",

    data(){
        return {

            // Input user
            userInput: "",

            // Array film
            arrayMovie: [],

            // Array tv
            arrayTv: [],

            // Array film popolari
            arrayMoviePopular: [],

            // Array Serie tv popolari
            arrayTvPopular: [],

            // Classe active menu ul 1
            activeMenu1: false,

            // Classe active menu ul 2
            activeMenu2: false,
        }
    },

    methods: {

        // Chiamata server movie
        getServerMovies: function() {
            // Svuoto l'array movie popular e tv popular
            this.arrayMoviePopular.splice(0, this.arrayMoviePopular.length);
            this.arrayTvPopular.splice(0, this.arrayTvPopular.length);

            // Imposto active menu 1 e 2 false
            this.activeMenu1 = false;
            this.activeMenu2 = false;

            axios.get("https://api.themoviedb.org/3/search/movie", {
                params: {
                    api_key: "fb43e793fe97fd60ade4def79dc2a4d7",
                    query: this.userInput,
                    language: "it",
                }
            })
            .then(res => {
                // console.log(res.data.results);
                this.arrayMovie = res.data.results;

                // Invio i dati dell'array al componente app con evento arrayMovie
                this.$emit("arrayMovie", this.arrayMovie);
            })

            .catch(error => {
                alert(error);
            })

        },

        // Chiamata server tv
        getServerTv: function () {
            // Svuoto l'array movie popular e tv popular
            this.arrayMoviePopular.splice(0, this.arrayMoviePopular.length);
            this.arrayTvPopular.splice(0, this.arrayTvPopular.length);

            // Imposto active menu 1 e 2 false
            this.activeMenu1 = false;
            this.activeMenu2 = false;

            axios.get("https://api.themoviedb.org/3/search/tv", {
                params: {
                    api_key: "fb43e793fe97fd60ade4def79dc2a4d7",
                    query: this.userInput,
                    language: "it",
                }
            })
            .then (response => {
                // console.log(res.data.results);
                this.arrayTv = response.data.results;

                 // Invio i dati dell'arrayTv al componente app con evento arrayTv
                this.$emit("arrayTv", this.arrayTv);

            })

            // Svuoto l'userInput
            this.userInput = "";
        },

        // Chiamata server film popolari
        getMoviePopular: function() {

            // Svuoto l'array film, serie tv e tv popular 
            this.arrayMovie.splice(0, this.arrayMovie.length);
            this.arrayTv.splice(0, this.arrayTv.length);
            this.arrayTvPopular.splice(0, this.arrayTvPopular.length);

            // Active menu 1 true
            this.activeMenu1 = true;

            // Active menu 2 false
            this.activeMenu2 = false;

            axios.get("https://api.themoviedb.org/3/movie/popular", {
                params: {
                    api_key: "fb43e793fe97fd60ade4def79dc2a4d7",
                    query: this.userInput,
                    language: "it",
                }
            })
            .then (response => {
                // console.log(response.data.results);
                this.arrayMoviePopular = response.data.results;
                
                // Invio i dati dell'arrayMoviePopular al componente app con evento arrayMoviePopular
                this.$emit("arrayMoviePopular", this.arrayMoviePopular);

            })
        },

        // Chiamata server serie tv popolari
        getTvPopular: function() {
            // Svuoto l'array film, serie tv e film popolari
            this.arrayMovie.splice(0, this.arrayMovie.length);
            this.arrayTv.splice(0, this.arrayTv.length);
            this.arrayMoviePopular.splice(0, this.arrayMoviePopular.length);

            // Active menu 1 false
            this.activeMenu1 = false;

            // Active menu 2 true    
            this.activeMenu2 = true;

            axios.get("https://api.themoviedb.org/3/tv/popular", {
                params: {
                    api_key: "fb43e793fe97fd60ade4def79dc2a4d7",
                    query: this.userInput,
                    language: "it",
                }
            })
            .then (response => {
                // console.log(response.data.results);
                this.arrayTvPopular = response.data.results;
               
                // Invio i dati dell'arrayTvPopular al componente app con evento arrayTvPopular
                this.$emit("arrayTvPopular", this.arrayTvPopular);

            })
        }
    }
}
</script>



<style lang="scss" scoped>
// Import common scss
@import '../assets/scss/common.scss';

.header_wrapper {
    display: flex;
    align-items: center;
    gap: 45px;
    flex-wrap: wrap;


    .logo_wrapper {
        display: flex;
        align-items: center;
        gap: 8px;
    
        img{
            width: 130px;
            filter: drop-shadow($text-shadow-black);
        }
    
        h1 {
            text-transform: uppercase;
            color: $color-red;
            text-shadow: 0 0 5px $color-red;
        }
    }

    ul {
        color: $color-white;
        display: flex;
        flex-wrap: wrap;
        gap: 40px;

        li {
            font-size: 22px;
            cursor: pointer;

            &:hover {
                color: $color-green;
                text-shadow: 0 0 4px $color-green;
                transition: all 280ms linear;
            }

            &.active {
                color: $color-green;
                text-shadow: 0 0 4px $color-green;
            }
        }
    }

    .search_btn_wrapper {
        flex-grow: 1;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 15px;

        input {
            max-width: 600px;
            height: 38px;
            flex-grow: 1;
            border: none;
            border-radius: 30px;
            padding-left: 20px;
            background-color: $color-gray;
            color: $color-white;
            filter: drop-shadow($text-shadow-black);
        }

        button {
            padding: 8px 15px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            background-color: $color-green;
            opacity: 0.5;
            filter: drop-shadow($text-shadow-black);

            &:hover {
                opacity: 1;
                transition: all 280ms linear;
            }

            img {
                width: 22px;
                height: 22px;
            }
        }
    }

}



</style>