<template>
  <div id="app">
    <main-tab-bar></main-tab-bar>
    <keep-alive exclude="Detail">
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
import MainTabBar from '@/components/content/mainTabbar/MainTabBar'
export default {
  data () {
    return {
    }
  },
  components: {
    MainTabBar
  },
  methods: {
  }
}

</script>
<style>
  @import "./assets/css/base.css";
</style>
