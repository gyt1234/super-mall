<template>
  <div v-if="Object.keys(detailInfo).length !==0">
    <img v-for="(item,index) in detailInfo.detailImage[0].list" :key="index" :src="item" @load="detailGoodsImage">
  </div>
</template>

<script>
export default {
  name: 'DetailGoodsInfo',
  props: {
    detailInfo: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  data () {
    return {
      counter: 0,
      imagesLength: 0
    }
  },
  methods: {
    detailGoodsImage () {
      // 所有图片都加载完了就进行一次回调
      if (++this.counter === this.imagesLength) {
        this.$emit('imageLoad')
      }
    }
  },
  watch: {
    detailInfo () {
      this.imagesLength = this.detailInfo.detailImage[0].list.length
    }
  }
}
</script>

<style scoped>
  img{
    width: 100%;
  }
</style>
