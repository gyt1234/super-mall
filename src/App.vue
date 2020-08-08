<template>
  <div id="app">
    <tab-bar>
      <tab-bar-item path="/home">
        <template v-slot:item-icon>
          <img src="./assets/img/tabbar/home.svg" />
        </template>
        <template v-slot:item-icon-active>
          <img src="./assets/img/tabbar/active1.svg" />
        </template>
        <template v-slot:item-text>
          <div>首页</div>
        </template>
      </tab-bar-item>
      <tab-bar-item path="/category">
        <template v-slot:item-icon>
          <img src="./assets/img/tabbar/eye.svg" />
        </template>
        <template v-slot:item-icon-active>
          <img src="./assets/img/tabbar/active2.svg" />
        </template>
        <template v-slot:item-text>
          <div>分类</div>
        </template>
      </tab-bar-item>
      <tab-bar-item path="/shopcar">
        <template v-slot:item-icon>
          <img src="./assets/img/tabbar/shopcar.svg" />
        </template>
        <template v-slot:item-icon-active>
          <img src="./assets/img/tabbar/active3.svg" />
        </template>
        <template v-slot:item-text>
          <div>购物车</div>
        </template>
      </tab-bar-item>
      <tab-bar-item path="/profile">
        <template v-slot:item-icon>
          <img src="./assets/img/tabbar/user.svg" />
        </template>
        <template v-slot:item-icon-active>
          <img src="./assets/img/tabbar/active4.svg" />
        </template>
        <template v-slot:item-text>
          <div>我的</div>
        </template>
      </tab-bar-item>
    </tab-bar>
    <router-view></router-view>
  </div>
</template>

<script>
import TabBar from './components/tabbar/TabBar'
import TabBarItem from './components/tabbar/TabBarItem'

export default {
  data () {
    return {
    }
  },
  components: {
    TabBarItem,
    TabBar
  },
  methods: {
  }
}

</script>
<style>
  @import "./assets/css/base.css";
</style>
