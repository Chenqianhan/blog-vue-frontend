<template>
    <div class="m-content">
        <div class = "space">
            <div class = "earth">
               <img src="../assets/plane.png" alt="">
            </div>
            <div>
                <!--
                <h1 class="title">Qianhan's Space</h1>
                -->
                <h1 class="title"><span>QianHan</span> <span>Space</span></h1>
            </div>
        </div>
        <!--
        <div class="block">
            <el-avatar :size="50" :src="user.avatar"></el-avatar>
            <div>{{ user.username }}</div>
        </div>
        -->
        <!--
        <div class="maction">
            <span><el-link href="/blogs">主页</el-link></span>
            <el-divider direction="vertical"></el-divider>
            <span><el-link type="success" href="/blog/add">发表博客</el-link></span>

            <el-divider direction="vertical"></el-divider>
            <span v-show="!hasLogin"><el-link type="primary" href="/login">登录</el-link></span>

            <span v-show="hasLogin"><el-link type="danger" @click="logout">退出</el-link></span>
        </div>
        -->
    </div>
</template>

<script>
    export default {
        name: "Header",
        data() {
            return {
                user: {
                    username: 'Please log in'
                },
                hasLogin: false
            }
        },
        methods: {
            logout() {
                const _this = this
                _this.$axios.get("/logout", {
                    headers: {
                        "Authorization": localStorage.getItem("token")
                    }
                }).then(res => {
                    _this.$store.commit("REMOVE_INFO")
                    _this.$router.push("/login")
                })
            }
        },
        created() {
            if(this.$store.getters.getUser.username) {
                this.user.username = this.$store.getters.getUser.username
                this.hasLogin = true
            }
        }
    }
</script>

<style scoped>
    /*
    .title{
        color: #B3C0D1;
    }
     */
    .title{
        color: #222;
        font-size: 50px;
        float: left;

    }
    .title span{
        transition: 0.5s;
    }
    .title:hover span:nth-child(1){
        margin-right: 10px;
    }
    .title:hover span:nth-child(2){
        margin-left: 30px;
    }
    .title:hover span:nth-child(1)::after{
        content: "'s";
    }
    .title:hover span{
        color: white;
        text-shadow: 0 0 10px #ffff,
                     0 0 20px #ffff,
                     0 0 30px #ffff,
                     0 0 40px #ffff;
    }

    .m-content {
        max-width:100%;
        margin: 0 auto;
        text-align: center;
    }
    .maction {
        margin: 10px 0;
    }
    .space{
        width: 100%;
        height: 150px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: rgb(5, 2, 34);
    }

    .earth{
        width: 100px;
        height: 100px;


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
        width: 40px;
        height: 40px;
        position: absolute;
        top: 30px;
    }
    .earth::before{
        content: '';
        width: 100px;
        height: 100px;
        position: absolute;
        left: 0;
        top: 0;
        background-image: url(../assets/cloud.png);
        animation: bg 15s linear infinite;
    }
</style>