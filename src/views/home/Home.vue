<template>
    <div id="home">
      <nav-bar class="home-nav">
        <template v-slot:center>购物街</template>
      </nav-bar>
      <!-- tab栏切换 -->
      <tab-control
        :titles="['流行','新款','精选']"
        @tabClick="tabClick"
        ref="tabControl1"
        class="tab-control"
        v-show="isTabFixed"
      >
      </tab-control>
      <scroll
        class="content"
        ref="scroll"
        :probe-type="3"
        @scroll="contentScroll"
        :pull-up-load="true"
        @pullingUp="loadMore"
      >
        <!-- 轮播图 -->
        <swiper :lists="banners" @swiperImgLoad="swiperImgLoad"></swiper>
        <!-- 推荐模块 -->
        <recommend-view :recommends="recommends"></recommend-view>
        <feature-view></feature-view>
        <!-- tab栏切换 -->
        <tab-control
          :titles="['流行','新款','精选']"
          @tabClick="tabClick"
          ref="tabControl2"
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
      visible: false,
      tabOffsetTop: 0,
      isTabFixed: false
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
        // 完成上拉加载更多
        this.$refs.scroll.finishPullUpLoad()
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
      this.$refs.tabControl1.currentIndex = index
      this.$refs.tabControl2.currentIndex = index
    },
    /**
     * 点击返回顶部处理事件
     */
    backClick () {
      this.$refs.scroll.scrollTop(0, 0, 500)
    },
    /**
     * 监听滚动位置
     */
    contentScroll (position) {
      // 判断回到顶部按钮是否显示
      this.visible = (-position.y) > 1000
      // 判断tabControl是否吸顶
      this.isTabFixed = this.isTabFixed = (-position.y) > this.tabOffsetTop
    },
    /**
     * 上拉加载更多
     */
    loadMore () {
      this.getHomeGoods(this.currentType)
      // 加载完重新计算可滚动的高度
      this.$refs.scroll.scroll.refresh()
    },
    /**
     * 监听图片加载完再计算tabControl的offsetTop
     */
    swiperImgLoad () {
      // $el获取组件元素
      this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop
    }
  },
  created () {
    this.getHomeMultidata()
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  mounted () {

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
    /*在使用浏览器原生滚动时，为了使得导航不跟随滚动，使用如下样式*/
    /*position: fixed;*/
    /*top: 0;*/
    /*left: 0;*/
    /*right: 0;*/
    /*z-index: 9;*/
  }
  .tab-control{
    position: relative;
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
</style>
