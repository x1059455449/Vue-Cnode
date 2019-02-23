<template>
  <div id="app">
    <Header></Header>
    <div class="main">
      <!-- <PostList></PostList> -->
      <!-- 此处的name="main"指向路由的components中的main -->
      <router-view name="slidebar"></router-view>
      <router-view name="main"></router-view>
      
    </div>
  </div>
</template>

<script>
import Header from './components/Header'
import PostList from './components/PostList'
import Article from './components/Article'
import UserInfo from './components/UserInfo'
import SlideBar from './components/SlideBar'
import Pagination from './components/Pagination'

export default {
  name: 'App',
  components:{
    Header,
    PostList,
    Article,
    UserInfo,
    SlideBar,
    Pagination
  }
}
</script>

<style>
.main {
  width: 100%;
  margin: 0 auto;
} 
</style>
