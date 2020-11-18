<template>
    <div>


        <div class="m-content">

            <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
                <el-form-item label="title" prop="title">
                    <el-input v-model="ruleForm.title"></el-input>
                </el-form-item>

                <el-form-item label="content" prop="content">
                    <mavon-editor v-model="ruleForm.content"></mavon-editor>
                </el-form-item>

                <el-form-item>
                    <el-button type="primary" @click="submitForm('ruleForm')">Create</el-button>
                    <el-button @click="resetForm('ruleForm')">Reset</el-button>
                </el-form-item>
            </el-form>

        </div>



    </div>
</template>

<script>
    import Header from "../components/Header";
    export default {
        name: "BlogEdit.vue",
        components: {Header},
        data() {
            return {
                ruleForm: {
                    id: '',
                    title: '',
                    content: ''
                },
                rules: {
                    title: [
                        { required: true, message: 'Please enter title', trigger: 'blur' },
                        { min: 3, max: 25, message: '3 to 25 character', trigger: 'blur' }
                    ],
                    content: [
                        { trequired: true, message: 'Please enter content', trigger: 'blur' }
                    ]
                }
            };
        },
        methods: {
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        const _this = this
                        this.$axios.post('/blog/edit', this.ruleForm, {
                            headers: {
                                "Authorization": localStorage.getItem("token")
                            }
                        }).then(res => {
                            console.log(res)
                            _this.$alert('succeed', 'Message', {
                                confirmButtonText: 'Close',
                                callback: action => {
                                    _this.$router.push("/blogs")
                                }
                            });
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
        },
        created() {
            const blogId = this.$route.params.blogId
            console.log(blogId)
            const _this = this
            if(blogId) {
                this.$axios.get('/blog/' + blogId).then(res => {
                    const blog = res.data.data
                    _this.ruleForm.id = blog.id
                    _this.ruleForm.title = blog.title
                    _this.ruleForm.content = blog.content
                })
            }
        }
    }
</script>

<style scoped>
    .m-content {
        text-align: center;
    }

    .demo-ruleForm{
        max-width: 1000px;
        max-height: 1000px;
        margin: 0 auto;
    }
</style>