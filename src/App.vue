<template>
  <div id="app">
    <!-- 首页跳转到关于页面，不加keep-alive首页就会销毁 再次进去就重新创建 滚动条回到最上方 
       排除Detail  因为详情页每次进入要新的数据，建新的组件，所以不要让detail keep-alive
    -->
    <keep-alive exclude="Detail">
      <router-view/>
    </keep-alive>
    <main-tab-bar/>
  </div>
</template>

<script>
import MainTabBar from 'components/content/mainTabbar/MainTabBar'

export default {
  name: 'App',
  components: {
    MainTabBar
  }
}
</script>

<style>
@import "assets/css/base.css"
</style>
