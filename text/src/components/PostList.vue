<template>
    <div class="PostList">
        <div class="loading" v-if="isLoading">
            <!-- 在数据未返回的时候，显示这个正在加载的gif -->
            <img src="../assets/loading.gif" alt="">
        </div>
        <!-- 下面div代表帖子主题 -->
        <div class="posts" v-else>
            <ul>
                <li>
                    <div class="toobar">
                        <span>全部</span>
                        <span>精华</span>
                        <span>分享</span>
                        <span>问答</span>
                        <span>招聘</span>
                    </div>
                </li>
                <li v-for="post in posts" :key="post.Avatar">
                    <img :src="post.author.avatar_url" alt="">
                    <span class="allcount">
                        <span class="reply_count">{{post.reply_count}}</span>
                        /{{post.visit_count}}
                    </span>
                    <span :class="[{put_good:(post.good == true),
                    put_top:(post.top == true),
                    'topiclist-tab':(post.good  != true && post.top  != true)}]">
                        <span>
                            {{post | tabFormatter}}
                        </span>
                    </span>
                    <router-link :to="{
                        name:'post_content',
                        params:{
                            id:post.id,
                            name:post.author.loginname
                        }
                    }">
                        <span>{{post.title}}</span>
                    </router-link>
                    <span class="last_reply">
                        {{post.last_reply | formatDate}}
                    </span>
                </li>
                <li>
                    <pagination @handleList="renderList"></pagination>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import pagination from './Pagination'
    export default {
        name:'PostList',
        data () {
            return {
                isLoading:false,
                posts:[],
                postpage:1
            }
        },
        components:{
            pagination
        },
        methods:{
            getData() {
                this.$http.get('https://cnodejs.org/api/v1/topics',{
                    params:{
                        page:this.postpage,
                        limit:15
                    }
                })
                .then(res => {
                    this.isLoading = false
                    this.posts = res.data.data
                })
                .catch(function (err) {
                    console.log(err)
                })
            },
            renderList(value) {
                this.postpage = value
                this.getData()
            }
        },
        beforeMount() {
            this.isLoading = true
            this.getData()
        }
    }
</script>

<style scoped>
.PostList {
    background-color: #e1e1e1;
}
.posts {
    margin-top: 10px;
}
.PostList img {
    width: 30px;
    height: 30px;
    vertical-align: middle;
}
ul {
    list-style: none;
    width: 100%;
    max-width: 1344px;
    margin: 0 auto;
}
ul li:not(:first-child) {
    padding: 9px;
    font-size: 15px;
    font-family: "Helvetica Neue", "Luxi Sans", "DejaVu Sans", Tahoma, "Hiragino Sans GB", STHeiti, sans-serif !important;
    font-weight: 400;
    background-color: white;
    color: #333;
    border-top: 1px solid #f0f0f0;
}
li:not(:first-child):hover {
    background: #f5f5f5;
}
li:last-child:hover {
    background: white;
}
li span {
    line-height: 30px;
}
.allcount {
    width: 70px;
    display: inline-block;
    text-align: center;
    font-size: 12px;
}
.reply_count {
    font-size: 14px;
    color: #987ec0;
}
.put_good ,.put_top {
    background: #80bd01;
    padding: 2xp 4px;
    border-radius: 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    -o-border-radius: 3px;
    color: #fff;
    font-size: 12px;
    margin-right:  10px;
}
.topiclist-tab {
    background-color: #e5e5e5;
    color: #999;
    padding: 2px 4px;
    border-radius: 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    -o-border-radius: 3px;
    font-size: 12px;
    margin-right: 10px;
}
.last_reply {
    text-align: right;
    min-width: 50px;
    display: inline-block;
    white-space: nowrap;
    float: right;
    color: #778087;
    font-size: 12px;
}
.toobar {
    height: 40px;
    background-color: #f5f5f5;
}
.toobar span {
    font-size: 14px;
    color: #80bd01;
    line-height: 40px;
    margin: 0 10px;
    cursor: pointer;
}
.toobar span:hover {
    color: #987ec0;
}
a {
    text-decoration: none;
    color: black;
}
a:hover {
    text-decoration: underline;
}
.loading {
    text-align: center;
    padding-top: 300px;
}
</style>
