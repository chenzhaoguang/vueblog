<template>
    <div class="m-content">
        <h3>欢迎来到陈昭光的博客</h3>
        <div class="block">
            <el-avatar :size="50" :src="user.avatar"></el-avatar>
            <div>{{ user.username }}</div>
        </div>

        <div class="maction">
            <span>
                <router-link :to="'/blogs'"><el-link>主页</el-link></router-link>
            </span>
            <el-divider direction="vertical"></el-divider>
            <span>
                <router-link :to="'/blog/add'">
                    <el-link type="success">发表博客</el-link>
                </router-link>
            </span>
            <el-divider direction="vertical"></el-divider>
            <span v-show="!hasLogin">
                <router-link :to="'/login'"><el-link type="primary">登录</el-link></router-link>
            </span>
            <span v-show="hasLogin"><el-link type="danger" @click="logout">退出</el-link></span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Header',
    data() {
        return {
            user: {
                username: '请先登录',
                avatar: 'https://open-prd.oss-cn-hzfinance.aliyuncs.com/dm-account/headimg/wI2JnwihmMjczbI5E3HJqK51tasPhFB0.png',
                // avatar: 'http://47.102.113.93/static/ameng/img/ameng.jpg',
            },
            hasLogin: false,
        }
    },
    methods: {
        logout() {
            const _this = this
            _this.$axios
                .get('/logout', {
                    headers: {
                        Authorization: localStorage.getItem('token'),
                    },
                })
                .then(res => {
                    _this.$store.commit('REMOVE_INFO')
                    _this.$router.push('/login')
                })
        },
    },
    created() {
        if (this.$store.getters.getUser.username) {
            this.user.username = this.$store.getters.getUser.username
            this.user.avatar = this.$store.getters.getUser.avatar

            this.hasLogin = true
        }
    },
}
</script>

<style scoped>
.m-content {
    max-width: 960px;
    margin: 0 auto;
    text-align: center;
}
.maction {
    margin: 10px 0;
}
</style>
