<template>
    <div id="home">
      <nav-bar class="home-nav">
        <template v-slot:center>购物街</template>
      </nav-bar>
      <!-- 轮播图 -->
      <swiper :lists="banners"></swiper>
      <!-- 推荐模块 -->
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <ul>
        <li>1</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
        <li>2</li>
      </ul>
    </div>
</template>

<script>
import NavBar from '@/components/common/navbar/NavBar'
import { getHomeMultidata } from '@/network/home'
import Swiper from '@/components/common/swiper/Swiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

export default {
  name: 'Home',
  components: {
    NavBar,
    Swiper,
    RecommendView,
    FeatureView
  },
  data () {
    return {
      banners: [],
      recommends: []
    }
  },
  created () {
    /**
     * 请求多个数据
     */
    getHomeMultidata().then(res => {
      this.banners = res.data.banner.list
      this.recommends = res.data.recommend.list
    })
  }
}
</script>

<style scoped>
  #home{
    padding-top: 44px;
  }
  .home-nav{
    background-color: var(--color-tint);
    color: white;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 9;
  }
</style>
