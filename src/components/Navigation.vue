<template>
    <div>
        <el-menu
                :default-active="activeIndex2"
                class="el-menu-demo"
                mode="horizontal"
                @select="handleSelect"
                background-color="#545c64"
                text-color="#fff"
                active-text-color="#ffd04b">

            <el-menu-item @click="intro">
                Intro
            </el-menu-item>

            <el-menu-item index="1" @click="toBlog">
                Blog
            </el-menu-item>

            <el-menu-item index="2" @click="toLibrary">
                Library
            </el-menu-item>

            <el-menu-item index="3" @click="toLogin">
                Login
            </el-menu-item>

            <el-menu-item @click="toScreenLock" v-loading.fullscreen.lock="fullscreenLoading">
                Try it
            </el-menu-item>

        </el-menu>
    </div>
</template>

<script>
    export default {
        name: "Navigation",
        data() {
            return {
                activeIndex: '1',
                activeIndex2: '1',
                fullscreenLoading: false
            };
        },
        methods: {
            handleSelect(key, keyPath) {
                console.log(key, keyPath);
            },

            intro(){
                this.$alert('Forgive me for my bothersome message box. ' +
                    'This website is just a blank template I made. I am learning how to develop frontend recently. ' +
                    'Features are coming!!!', 'Intro', {
                    confirmButtonText: 'Close',
                    callback: action => {
                        this.$message({
                            type: 'info',
                            message: `Try to hover on "Qianhan Space!!!" `
                        });
                    }
                });
            },
            toBlog(){
                this.$router.push("/blog").catch(err => {err});
            },
            toLogin(){
                this.$router.push("/login").catch(err => {err});
            },
            toLibrary(){
                this.$message("Not available now");
            },
            toScreenLock(){
                const loading = this.$loading({
                    lock: true,
                    text: 'There is no loading but only make you uncomfortable'
                });
                setTimeout(() => {
                    loading.close();
                }, 3000);
            }

        }

    }
</script>

<style scoped>

</style>