<template>
    <div id="mainBanner">
        <h1>Make Your Burger</h1>
    </div>
</template>

<script>
    export default {
        name: "Banner"
    }
</script>

<style scoped>
    #mainBanner {
        background-image: url("../../public/img/burguer.jpg");
        background-position: 0 ;
        background-size: cover;
        height: 625px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #mainBanner h1 {
        color: #fff;
        text-align: center;
        font-size: 60px;
        background-color: #222;
        padding: 20px 40px;
    }
</style>