<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  name: 'Scroll',
  props: {
    // 是否实时监听 为3时实时监听
    probeType: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      scroll: null
    }
  },
  mounted () {
    // 创建BScroll对象
    this.scroll = new BScroll(this.$refs.wrapper, {
      // 使得div标签可以点击
      click: true,
      probeType: this.probeType
    })
    // 实时监听滚动的位置
    this.scroll.on('scroll', (position) => {
      this.$emit('scroll', position)
    })
  },
  methods: {
    /**
     * 回到顶部 第一个和第二个参数是回到顶部的x轴和y轴的位置，第三个参数是回到顶部的时间
     */
    scrollTop (x, y, time = 300) {
      this.scroll.scrollTo(x, y, time)
    }
  }
}
</script>

<style scoped>

</style>
