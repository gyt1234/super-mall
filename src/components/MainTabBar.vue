<template>
  <tab-bar>
    <tab-bar-item path="/home" activeColor="#00a6ff">
      <template v-slot:item-icon>
        <img src="@/assets/img/tabbar/home.svg" />
      </template>
      <template v-slot:item-icon-active>
        <img src="@/assets/img/tabbar/active1.svg" />
      </template>
      <template v-slot:item-text>
        <div>首页</div>
      </template>
    </tab-bar-item>
    <tab-bar-item path="/category" activeColor="#00a6ff">
      <template v-slot:item-icon>
        <img src="@/assets/img/tabbar/eye.svg" />
      </template>
      <template v-slot:item-icon-active>
        <img src="@/assets/img/tabbar/active2.svg" />
      </template>
      <template v-slot:item-text>
        <div>分类</div>
      </template>
    </tab-bar-item>
    <tab-bar-item path="/shopcar" activeColor="#00a6ff">
      <template v-slot:item-icon>
        <img src="@/assets/img/tabbar/shopcar.svg" />
      </template>
      <template v-slot:item-icon-active>
        <img src="@/assets/img/tabbar/active3.svg" />
      </template>
      <template v-slot:item-text>
        <div>购物车</div>
      </template>
    </tab-bar-item>
    <tab-bar-item path="/profile" activeColor="#00a6ff">
      <template v-slot:item-icon>
        <img src="@/assets/img/tabbar/user.svg" />
      </template>
      <template v-slot:item-icon-active>
        <img src="@/assets/img/tabbar/active4.svg" />
      </template>
      <template v-slot:item-text>
        <div>我的</div>
      </template>
    </tab-bar-item>
  </tab-bar>
</template>

<script>
import TabBar from '@/components/tabbar/TabBar'
import TabBarItem from '@/components/tabbar/TabBarItem'
export default {
  name: 'MainTabBar',
  components: {
    TabBarItem,
    TabBar
  }
}
</script>

<style scoped>

</style>
