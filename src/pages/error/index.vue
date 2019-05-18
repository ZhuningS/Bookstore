<template>
  <div class="container ub-box">
    <dl class="ub-box ub-col ub-ver z-width-100-percent" style="background:#fff">
      <i class="z-margin-bottom-20-px iconfont icon-jijianfasong z-font-size-60" style="color:#c11c06"></i>
      <span class="z-font-size-15 z-color-888">HELLOWORLD</span>
    </dl>
  </div>
</template>
<script>
export default {
  data () {
    return {}
  },
  methods: {},
  onShow () {
    wx.setNavigationBarTitle({title: '正在开发'})
  }
}
</script>
<style scoped>
  .container{width:100%;height:100vh;background:#fff;}
</style>
