<template>
    <div id="home">
      <!-- 导航 -->
      <nav-bar class="home-nav">
        <template v-slot:center>购物街</template>
      </nav-bar>
      <!-- 轮播图 -->
      <swiper :lists="banners"></swiper>
    </div>
</template>

<script>
import NavBar from '@/components/common/navbar/NavBar'
import { getHomeMultidata } from '@/network/home'
import Swiper from '@/components/common/swiper/Swiper'

export default {
  name: 'Home',
  components: {
    NavBar,
    Swiper
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
