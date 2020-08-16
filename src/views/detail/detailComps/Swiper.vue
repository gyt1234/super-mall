<template>
  <div class="block">
    <el-carousel trigger="click" height="300px">
      <el-carousel-item v-for="(list,index) in lists" :key="index">
        <img :src="list">
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
  }
}
</script>

<style scoped>
  .el-carousel__item img {
    margin: 0;
    height: 300px;
    width: 100%;
  }
</style>
