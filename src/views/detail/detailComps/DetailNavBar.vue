<template>
  <div>
    <nav-bar>
      <template v-slot:left>
        <img src="@/assets/img/common/back.svg" class="backImg" @click="backClick">
      </template>
      <template v-slot:center>
        <div  class="title">
          <div
            v-for="(item,index) in titles"
            :key="index"
            class="title-item"
            :class="{active: index === currentIndex}"
            @click="titleClick(index)"
          >
            {{item}}
          </div>
        </div>
      </template>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from '@/components/common/navbar/NavBar'
export default {
  name: 'DetailNavBar',
  components: {
    NavBar
  },
  data () {
    return {
      titles: ['商品', '参数', '评论', '推荐'],
      currentIndex: 0
    }
  },
  methods: {
    /**
     * tab导航栏切换
     */
    titleClick (index) {
      this.currentIndex = index
    },
    /**
     * 点击返回按钮
     */
    backClick () {
      this.$router.go(-1)
    }
  }
}
</script>

<style scoped>
  .title{
    display: flex;
  }
  .title-item{
    flex: 1;
  }
  .active{
    color: var(--color-high-text);
  }
  .backImg{
    margin-top: 10px;
  }
</style>
