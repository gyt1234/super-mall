<template>
  <div id="detail">
    <detail-nav-bar></detail-nav-bar>
    <swiper :lists="topImages" height="150"></swiper>
  </div>
</template>

<script>
import DetailNavBar from './detailComps/DetailNavBar'
import { getDetail } from '@/network/detail.js'
import Swiper from './detailComps/Swiper'

export default {
  name: 'Detail',
  components: {
    DetailNavBar,
    Swiper
  },
  data () {
    return {
      iid: '',
      topImages: []
    }
  },
  methods: {
    /**
     * 根据id请求详情数据
     */
    getDetail () {
      getDetail(this.iid).then(res => {
        this.topImages = res.result.itemInfo.topImages.slice(0, 4)
        console.log(this.topImages)
      })
    }
  },
  created () {
    this.iid = this.$route.params.iid
    this.getDetail()
  }
}
</script>

<style scoped>

</style>
