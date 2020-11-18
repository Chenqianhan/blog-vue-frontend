<template>
    <div class = "earth">
        <img src="../assets/plane.png" alt="">
    </div>
</template>

<script>
    export default {
        name: "Earth.vue"
    }
</script>

<style scoped>
    body{
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: rgb(5, 2, 34);
    }
    .earth{
        width: 200px;
        height: 200px;
        border-radius: 50%;
        background: #0588e4 url(../assets/earth.png);
        background-size: cover;
        display: flex;
        justify-content: center;
        align-item: center;
        position: relative;
        overflow: hidden;
        box-shadow: 0 0 60px rgba(0,0,0,0.7);
        animation: bg 12s linear infinite;
    }
    @keyframes bg {
        from{
            background-position: 0 0;
        }
        to{
            background-position: 719px 0;
        }
    }
    .earth img{
        width: 100px;
        height: 100px;
    }
    .earth::before{
        content: '';
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        background-image: url(../assets/cloud.png);
        animation: bg 15s linear infinite;
    }
</style>