<template>
    <div id="home">
      <nav-bar class="home-nav">
        <template v-slot:center>购物街</template>
      </nav-bar>
      <scroll class="content" ref="scroll" :probe-type="3" @scroll="contentScroll">
        <!-- 轮播图 -->
        <swiper :lists="banners"></swiper>
        <!-- 推荐模块 -->
        <recommend-view :recommends="recommends"></recommend-view>
        <feature-view></feature-view>
        <!-- tab栏切换 -->
        <tab-control
          :titles="['流行','新款','精选']"
          class="tab-control"
          @tabClick="tabClick"
        >
        </tab-control>
        <goods-list :goods="showGoods"></goods-list>
      </scroll>
      <back-top @click.native="backClick" v-show="visible"></back-top>
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
import BackTop from '@/components/content/backTop/BackTop'

// 导入封装好的滚动
import Scroll from '@/components/common/scroll/Scroll'

export default {
  name: 'Home',
  components: {
    NavBar,
    Swiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList,
    Scroll,
    BackTop
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
      currentType: 'pop',
      visible: false
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
    },
    /**
     * 点击返回顶部处理事件
     */
    backClick () {
      this.$refs.scroll.scrollTop(0, 0, 500)
    },
    /**
     * 监听滚动位置判断回到顶部按钮的显示与隐藏
     */
    contentScroll (position) {
      this.visible = (-position.y) > 1000
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
    /*padding-top: 44px;*/
    /* 当前视口高度 100vh意思是100%的视口高度 */
    height: 100vh;
    position:relative;
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
  .content{
    overflow: hidden;
    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }
  /*.content{*/
  /*  height: calc(100% - 93px);*/
  /*  overflow: hidden;*/
  /*  margin-top: 44px;*/
  /*}*/
</style>
