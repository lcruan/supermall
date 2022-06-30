<template>
    <div id="home">
        <!-- 这里面要插入内容 -->
        <nav-bar class="home-nav">
            <div slot="center">购物街</div>
        </nav-bar>
        <home-swiper :banners="banners"/>
    </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
import HomeSwiper from './childComps/HomeSwiper'
// 这里不是default导出 所以用大括号导入
import {getHomeMultidata} from 'network/home'

export default {
    name: 'Home',
    data() {
        return {
            // 函数getHomeMultidata里面的数据执行完后，会被回收，所以在定义一个data用于存放获取的数据
            banners: [],
            recommends: []
        }
    },
    components: {
        NavBar,
        HomeSwiper
    },
    //组件创建好之后，发送请求
    created() {
        // 1. 请求多个数据
        getHomeMultidata().then(res => {
            this.banners = res.data.banner.list;
            this.recommends = res.data.recommend;
        });
    }
}
</script>

<style>
.home-nav {
    background-color: var(--color-tint);
    color: #fff;
}
</style>