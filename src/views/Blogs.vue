<template>
    <div class="mcontaner">
        <Header>Quainhan's Blog</Header>
        <Navigation></Navigation>
        <el-container>
            <el-main>
                <div class="block">
                    <el-timeline>
                        <el-timeline-item :timestamp="blog.date" placement="top" v-for="blog in blogs">
                            <!--
                            <el-card >
                                <h1>
                                    <router-link :to="{name: 'BlogDetail', params: {blogId: blog.id}}">
                                        {{blog.title}}
                                    </router-link>
                                </h1>
                            </el-card>
                            -->
                            <!--
                            <el-card class = "box-card">
                                <div slot = "header" class="clearfix">
                                    <span>{{blog.title}}</span>
                                    <el-button class="el-icon-edit-outline"></el-button>
                                </div>
                            </el-card>
                            -->

                            <el-collapse accordion>
                                <el-collapse-item>
                                    <template slot = "title">
                                        <h1 class = "txt">
                                            {{blog.title}}
                                        </h1>
                                    </template>
                                    <div>{{blog.content}}</div>
                                    <div>
                                        <el-button class="el-icon-edit-outline" @click = "msg" />
                                    </div>
                                </el-collapse-item>
                            </el-collapse>

                            <!--
                            <el-collapse v-model="activeNames" @change="handleChange">
                                <el-collapse-item name="1">
                                    <div>{{blog.content}}</div>
                                </el-collapse-item>
                            </el-collapse>
                            -->
                        </el-timeline-item>

                    </el-timeline>

                    <el-pagination class="mpage"
                                   background
                                   layout="prev, pager, next"
                                   :current-page="currentPage"
                                   :page-size="pageSize"
                                   :total="total"
                                   @current-change=page>
                    </el-pagination>

                </div>
            </el-main>
            <el-footer>Footer</el-footer>
        </el-container>


    </div>
</template>

<script>
    import Header from "../components/Header";
    import Navigation from "../components/Navigation";
    export default {
        name: "Blogs.vue",
        components: {Header, Navigation},
        data() {
            return {
                blogs: {},
                currentPage: 1,
                total: 0,
                pageSize: 10
            }
        },
        methods: {
            page(currentPage) {
                const _this = this
                _this.$axios.get("/blog?currentPage=" + currentPage).then(res => {
                    console.log(res)
                    _this.blogs = res.data.data.records
                    _this.currentPage = res.data.data.current
                    _this.total = res.data.data.total
                    _this.pageSize = res.data.data.size

                })
            },

            msg(){
                this.$message("No permission...")
            }
        },
        created() {
            this.page(1)
        }
    }
</script>

<style scoped>
    .mpage{
        margin: 0 auto;
        text-align: center;
    }

    .txt{
        front-family: "Helvetica Neue";
        text-align: center;

    }

    .clearfix:before,
    .clearfix:after {
        display: table;
        content: "";
    }
    .clearfix:after {
        clear: both;
    }

    .box-card {
        width: 100%;
    }

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
</style>