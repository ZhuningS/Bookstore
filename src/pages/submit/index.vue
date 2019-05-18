<template>
  <div class="container ub-box">
   <dl class="ub-box ub-col z-width-100-percent">
    <dd class="item z-width-100-percent ub-box ub-ver ub-between z-box-sizing-border z-bg-color-fff">
      <span class="z-font-size-15 z-color-333 z-font-weight-bold">{{formdata.mainTitle}}</span>
      <span class="z-font-size-15 z-color-333 z-font-weight-bold">{{formdata.price}}元</span>
    </dd>
    <dd class="item z-width-100-percent ub-box ub-ver ub-between z-box-sizing-border z-bg-color-fff">
      <span class="z-font-size-15 z-color-333 z-font-weight-bold">数量</span>
      <span>
        <counter @counterService="counterService"></counter>
      </span>
    </dd>
    <dd class="item z-width-100-percent ub-box ub-ver ub-between z-box-sizing-border z-bg-color-fff">
      <span class="z-font-size-15 z-color-333 z-font-weight-bold">小计</span>
      <span class="z-font-size-15 z-font-weight-bold" style="color:red">
        ¥{{formdata.totalPrice}}
      </span>
    </dd>
    <!--fixed部分-->
    <ul class="fixCon ub-box ub-ver ub-between">
      <li class="ub-box ub-ver z-padding-h-10-px">
        <span class="z-font-size-12 z-color-999 z-margin-right-10-px">付款金额</span>
        <span class="z-font-size-18 z-font-weight-bold" style="color:red">¥{{formdata.totalPrice}}</span>
      </li>
      <li @click.stop="$openWin('/pages/error/main')" class="sumbitBtn ub-box ub-ver z-font-size-16 z-color-fff">提交订单</li>
    </ul>
   </dl>
  </div>
</template>
<script>
  import counter from "../../components/counter.vue"
  export default {
    components: {counter},
    data () {
      return {
        formdata: {
          goodId: '100',
          mainTitle: '时间简史',
          num: 1,
          price: 38.00,
          totalPrice: 38.00,
          phone: '123****9876',
        }
      }
    },
    methods: {
      counterService(n) {
        this.formdata.num = n
        this.formdata.totalPrice = (this.formdata.price|0) * n
      }
    },
    onShow() {
      wx.setNavigationBarTitle({title: '提交订单'})
    }
  }
</script>
<style scoped>
  .container{width:100%;height:100vh;background:#f5f5f5}
  .item{border-bottom: 1px solid #f5f5f5;padding: 10px 8px;}
  .fixCon{position: fixed;left: 0;bottom: 0;z-index: 10;width: 100%;background: #fff;}
  .sumbitBtn{padding: 15px 35px;background: #c11c06;box-sizing: border-box;}
</style>
