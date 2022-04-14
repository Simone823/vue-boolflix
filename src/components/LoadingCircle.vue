<template>

    <!-- Loading -->
    <div class="loading">
        <div class="circle"></div>
        <h2>Cerca un film, una serie tv o scegli per categoria</h2>
    </div>

</template>



<script>
export default {
    name: "LoadingCircle",
}
</script>



<style lang="scss" scoped>
// Import common scss
@import '../assets/scss/common.scss';

.loading {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translateX(-50%) translateY(-50%);
    display: flex;
    flex-direction: column;

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
</style>