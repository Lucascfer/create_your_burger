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
        background-image: url('../img/burguer.jpg');
        background-position: 0 - 250px;
        background-size: cover;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }
</style>