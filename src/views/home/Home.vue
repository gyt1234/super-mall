<template>
    <div>
      <nav-bar class="home-nav">
        <template v-slot:center>购物街</template>
      </nav-bar>
      <!-- 轮播图 -->
      <swiper :lists="banners"></swiper>
      <!-- 推荐模块 -->
      <recommend-view :recommends="recommends"></recommend-view>
    </div>
</template>

<script>
import NavBar from '@/components/common/navbar/NavBar'
import { getHomeMultidata } from '@/network/home'
import Swiper from '@/components/common/swiper/Swiper'
import RecommendView from './childComps/RecommendView'

export default {
  name: 'Home',
  components: {
    NavBar,
    Swiper,
    RecommendView
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
  .home-nav{
    background-color: var(--color-tint);
    color: white;
  }
</style>
