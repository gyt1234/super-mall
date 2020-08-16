<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav"></detail-nav-bar>
    <scroll class="content" ref="scroll">
      <swiper :lists="topImages" height="150"></swiper>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shop="shop"></detail-shop-info>
      <detail-goods-info :detail-info="detailInfo" @imageLoad="imageLoad"></detail-goods-info>
      <detail-param-info :paramInfo="paramInfo"></detail-param-info>
    </scroll>
  </div>
</template>

<script>
import DetailNavBar from './detailComps/DetailNavBar'
import { getDetail, Goods, Shop, GoodsParams } from '@/network/detail.js'
import Swiper from './detailComps/Swiper'
import DetailBaseInfo from './detailComps/DetailBaseInfo'
import DetailShopInfo from './detailComps/DetailShopInfo'
import Scroll from '@/components/common/scroll/Scroll'
import DetailGoodsInfo from './detailComps/DetailGoodsInfo'
import DetailParamInfo from './detailComps/DetailParamInfo'

export default {
  name: 'Detail',
  components: {
    DetailBaseInfo,
    DetailNavBar,
    Swiper,
    DetailShopInfo,
    Scroll,
    DetailGoodsInfo,
    DetailParamInfo
  },
  data () {
    return {
      iid: '',
      // 顶部轮播图片
      topImages: [],
      goods: {},
      shop: {},
      detailInfo: {},
      paramInfo: {}
    }
  },
  methods: {
    /**
     * 根据id请求详情数据
     */
    getDetail () {
      getDetail(this.iid).then(res => {
        const data = res.result
        // 获取顶部轮播图
        this.topImages = res.result.itemInfo.topImages.slice(0, 4)
        // 获取商品信息
        this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.service)
        // 获取店铺信息
        this.shop = new Shop(data.shopInfo)
        // 获取商品详情信息
        this.detailInfo = data.detailInfo
        // 获取参数信息
        this.paramInfo = new GoodsParams(data.itemParams.info, data.itemParams.rule)
      })
    },
    /**
     * 处理图片加载完
     */
    imageLoad () {
      this.$refs.scroll.scroll.refresh()
    }
  },
  created () {
    this.iid = this.$route.params.iid
    this.getDetail()
  }
}
</script>

<style scoped>
 #detail{
   position: relative;
   z-index: 30;
   background: #ffffff;
   height: 100vh;
 }
 .detail-nav{
   position: relative;
   z-index: 40;
   background: #ffffff;
 }
  .content{
    height: calc(100% - 44px);
  }
</style>
