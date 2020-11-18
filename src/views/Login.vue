<template>
    <div>
        <Header>Quainhan's Blog</Header>
        <Navigation></Navigation>
        <el-container>
            <el-main>
                <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
                    <el-form-item label="username" prop="username">
                        <el-input v-model="ruleForm.username"/>
                    </el-form-item>
                    <el-form-item label="password" prop="password">
                        <el-input type="password" v-model="ruleForm.password"/>
                    </el-form-item>

                    <el-form-item>
                        <el-button type="primary" @click="submitForm('ruleForm')">Sign in</el-button>
                        <el-button @click="resetForm('ruleForm')">Reset</el-button>
                    </el-form-item>
                </el-form>
            </el-main>
        </el-container>
    </div>
</template>

<script>
    import Header from "../components/Header";
    import Navigation from "../components/Navigation";
    export default {
        name: "Login",
        components: {Header, Navigation},
        data() {
            return {
                ruleForm: {
                    username: '',
                    password: '',
                },
                rules: {
                    username: [
                        { required: true, message: 'Username required', trigger: 'blur' },
                        { min: 3, max: 15, message: 'Username length is 3 to 15', trigger: 'blur'}
                    ],
                    password: [
                        { required: true, message: 'Password required', trigger: 'blur' }
                    ],
                }
            };
        },
        methods: {
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        const _this = this
                        this.$axios.post('/login', this.ruleForm).then(res => {
                            console.log(res.data)
                            const jwt = res.headers['authorization']
                            const userInfo = res.data.data

                            //Put session in local store rather than cookie
                            _this.$store.commit("SET_TOKEN", jwt)
                            _this.$store.commit("SET_USERINFO", userInfo)

                            console.log(_this.$store.getters.getUser)

                            _this.$router.push("/blog")
                        })
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
            }
        }

    }
</script>

<style>
    .el-header, .el-footer {
        background-color: #B3C0D1;
        color: #333;
        text-align: center;
        line-height: 60px;
    }

    .el-aside {
        background-color: #D3DCE6;
        color: #333;
        text-align: center;
        line-height: 200px;
    }

    .el-main {
        background-color: #E9EEF3;
        color: #333;
        text-align: center;
        line-height: 160px;
    }

    body > .el-container {
        margin-bottom: 40px;
    }

    .el-container:nth-child(5) .el-aside,
    .el-container:nth-child(6) .el-aside {
        line-height: 260px;
    }

    .el-container:nth-child(7) .el-aside {
        line-height: 320px;
    }

    .demo-ruleForm {
        max-width: 400px;
        margin: 0 auto;
    }
</style>