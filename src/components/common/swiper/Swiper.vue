<template>
  <div class="block">
    <el-carousel trigger="click" height="150px">
      <el-carousel-item v-for="(list,index) in lists" :key="index">
        <a :href="list.link"><img :src="list.image" @load="imageLoad"></a>
      </el-carousel-item>
    </el-carousel>
  </div>
</template>

<script>
export default {
  name: 'Swiper',
  props: {
    lists: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      isLoad: false
    }
  },
  methods: {
    /**
     * 监听图片是否加载完成(只需要发出一次事件)
     */
    imageLoad () {
      if (!this.isLoad) {
        this.$emit('swiperImgLoad')
        this.isLoad = true
      }
    }
  }
}
</script>

<style scoped>
  .el-carousel__item img {
    margin: 0;
    height: 150px;
    width: 100%;
  }
</style>
