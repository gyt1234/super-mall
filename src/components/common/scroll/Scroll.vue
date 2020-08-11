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
    // 判断是否实时监听 为3时实时监听
    probeType: {
      type: Number,
      default: 0
    },
    // 判断是否要上拉加载更多
    pullUpLoad: {
      type: Boolean,
      default () {
        return {}
      }
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
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad
    })
    // 实时监听滚动的位置
    this.scroll.on('scroll', (position) => {
      this.$emit('scroll', position)
    })
    // 监听上拉加载更多事件
    this.scroll.on('pullingUp', () => {
      this.$emit('pullingUp')
    })
  },
  methods: {
    /**
     * 回到顶部 第一个和第二个参数是回到顶部的x轴和y轴的位置，第三个参数是回到顶部的时间
     */
    scrollTop (x, y, time = 300) {
      this.scroll.scrollTo(x, y, time)
    },
    /**
     * 完成下拉加载更多
     */
    finishPullUpLoad () {
      this.scroll.finishPullUp()
    }
  }
}
</script>

<style scoped>

</style>
