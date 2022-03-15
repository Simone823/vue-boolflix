<template>

    <!-- header Wrapper -->
    <div class="header_wrapper">

        <!-- Logo header -->
        <div class="logo_wrapper">
            <!-- Logo -->
            <img src="../assets/img/netflix_logo.png" alt="">

            <!-- Titolo -->
            <h1>Boolflix</h1>
        </div>

        <!-- Input text, button -->
        <div class="search_btn_wrapper">
            <!-- Input text -->
            <input type="text" placeholder="Digita il nome del film">

            <!-- Button -->
            <button>
                <img src="../assets/img/search_logo.png" alt="">
            </button>
        </div>

    </div>

</template>



<script>
export default {
    name: "LogoSearch",
}
</script>



<style lang="scss" scoped>
// Import common scss
@import '../assets/scss/common.scss';

.header_wrapper {
    display: flex;
    align-items: center;
    gap: 20px;


    .logo_wrapper {
        display: flex;
        align-items: center;
        gap: 8px;
    
        img{
            width: 65px;
            height: 65px;
            filter: drop-shadow(0 0 5px black);
        }
    
        h1 {
            text-transform: uppercase;
            color: $color-red;
            text-shadow: 0 0 5px black;
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
            filter: drop-shadow(0 0 5px black);
        }

        button {
            padding: 8px 15px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            background-color: $color-green;
            opacity: 0.5;
            filter: drop-shadow(0 0 5px black);

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