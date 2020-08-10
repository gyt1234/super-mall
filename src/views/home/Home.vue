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
      <tab-control
        :titles="['流行','新款','精选']"
        class="tab-control"
        @tabClick="tabClick"
      >
      </tab-control>
      <goods-list :goods="showGoods"></goods-list>
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
import { getHomeMultidata, getHomeGoods } from '@/network/home'
import Swiper from '@/components/common/swiper/Swiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'
import TabControl from '@/components/content/tabControl/TabControl'
import GoodsList from '@/components/content/goods/GoodsList'

export default {
  name: 'Home',
  components: {
    NavBar,
    Swiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList
  },
  data () {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      },
      currentType: 'pop'
    }
  },
  computed: {
    showGoods () {
      return this.goods[this.currentType].list
    }
  },
  methods: {
    /**
     * 请求轮播图以及推荐模块数据
     */
    getHomeMultidata () {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list
        this.recommends = res.data.recommend.list
      })
    },
    /**
     * 请求首页商品数据
     */
    getHomeGoods (type) {
      // 获取每一页的数据
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
      })
    },
    /**
     * 处理tab点击切换不同的商品
     */
    tabClick (index) {
      switch (index) {
        case 0:
          this.currentType = 'pop'
          break
        case 1:
          this.currentType = 'new'
          break
        case 2:
          this.currentType = 'sell'
          break
      }
    }
  },
  created () {
    this.getHomeMultidata()
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
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
  .tab-control{
    position: sticky;
    top: 44px;
    z-index: 9;
  }
</style>
