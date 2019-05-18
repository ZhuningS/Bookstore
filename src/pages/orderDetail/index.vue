<template>
  <div class="container ub-box">
    <scroll-view scroll-y style="height: 100vh" scroll-top="0">
     <dl class="ub-box ub-col z-width-100-percent">
      <dd class="item z-width-100-percent ub-box ub-ver z-box-sizing-border z-bg-color-fff">
        <p class="ub-box">
          <img class="z-img-cover" :src="formdata.img" />
        </p>
        <div class="ub-flex-1 ub-box ub-col z-padding-h-10-px z-box-sizing-border">
          <p class="z-font-size-15 z-color-333 z-margin-bottom-3-px z-font-weight-bold z-lines-1-overflow-hidden">{{formdata.mainTitle}}</p>
          <p class="z-font-size-14 z-color-666 z-margin-bottom-3-px z-lines-1-overflow-hidden">{{formdata.subTitle}}</p>
          <p class="z-font-size-14 z-margin-bottom-3-px" style="color:#c11c06">¥{{formdata.price}}</p>
        </div>
      </dd>
      <dd class="item z-margin-top-8-px z-width-100-percent ub-box ub-ver ub-col z-box-sizing-border z-bg-color-fff">
        <span class="z-font-size-15 z-color-333 z-margin-bottom-8-px z-font-weight-bold">图书信息</span>
        <span class="z-font-size-14 z-color-333 z-margin-bottom-8-px ">科技系列图书 中国科学出版社 作者：霍金</span>
        <div class="ub-box ub-ver ub-between z-width-100-percent z-border-bottom-1-eee z-padding-v-10-px">
          <span class="z-font-size-14 z-color-333">{{formdata.package.packageName}}</span>
          <span class="z-font-size-14 z-color-333">{{formdata.package.packagePrice}}</span>
        </div>
        <ul class="ub-box ub-col z-width-100-percent z-margin-top-8-px">
          <li v-for="(val, i) in formdata.package.notes" :key="i" class="z-font-size-14 z-color-333 z-lineHeight-22 z-margin-bottom-5-px">{{val}}</li>
        </ul>
      </dd>
      <dd style="padding:8px 50px" class="z-margin-top-8-px z-width-100-percent ub-box ub-ver ub-col z-box-sizing-border z-bg-color-fff">
        <span class="z-font-size-15 z-color-333 z-margin-bottom-8-px z-font-weight-bold">订单信息</span>
        <ul class="z-width-100-percent ub-box ub-col ub-ver">
          <li class="z-width-100-percent ub-box ub-between ub-ver z-margin-bottom-8-px">
            <span class="z-font-size-14 z-color-888 ub-flex-1 z-textAlign-left">订单号</span>
            <span class="z-font-size-14 z-color-888 ub-flex-2 z-textAlign-right">{{formdata.orderNum}}</span>
          </li>
          <li class="z-width-100-percent ub-box ub-between ub-ver z-margin-bottom-8-px">
            <span class="z-font-size-14 z-color-888 ub-flex-1 z-textAlign-left">手机号</span>
            <span class="z-font-size-14 z-color-888 ub-flex-2 z-textAlign-right">{{formdata.orderPhone}}</span>
          </li>

          <li class="z-width-100-percent ub-box ub-between ub-ver z-margin-bottom-8-px">
            <span class="z-font-size-14 z-color-888 ub-flex-1 z-textAlign-left">数量</span>
            <span class="z-font-size-14 z-color-888 ub-flex-2 z-textAlign-right">{{formdata.orderCount}}</span>
          </li>
          <li class="z-width-100-percent ub-box ub-between ub-ver">
            <span class="z-font-size-14 z-color-888 ub-flex-1 z-textAlign-left">总价</span>
            <span class="z-font-size-14 z-color-888 ub-flex-2 z-textAlign-right">{{formdata.orderTotalPrice}}</span>
          </li>
        </ul>
      </dd>
      <dd class="item z-margin-top-8-px z-width-100-percent ub-box ub-ver ub-col z-box-sizing-border z-bg-color-fff">
        <span class="z-font-size-15 z-color-333 z-margin-bottom-8-px z-font-weight-bold">小提示</span>
        <p class="z-font-size-14 z-color-999 z-lineHeight-22 z-margin-bottom-8-px">欢迎下次光临</p>
        <span @click.stop="clickContact()" class="contactBtn z-width-100-percent ub-box ub-ver z-font-size-14 z-color-666">联系客服</span>
      </dd>
     </dl>
    </scroll-view>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        formdata: {
          goodId: '100',
          mainTitle: '时间简史',
          subTitle: '时间简史',
          img: 'http://p0.meituan.net/200.0/deal/522fd16a9b25479496188b59476d1b941062402.jpg@206_0_828_828a%7C267h_267w_2e_90Q',
          sellerName: '时间简史',
          package: {
            packageName: '时间简史',
            packagePrice: '¥38',
            notes: [
              '备注：',
              '励志格言：知识就是力量',
            ],
          },
          sellerTel: '',
          price: 38.00,
          orderNum: '123456',
          orderPhone: '123****3468',
          orderCount: '1',
          orderTotalPrice: '38',
        }
      }
    },
    methods: {
      clickContact() {
        wx.showActionSheet({
          itemList: ['客服电话：7654321'],
          success(res) {
            switch(res.tapIndex) {
              case 0:
                wx.makePhoneCall({phoneNumber: '7654321'})
                break
            }
          }
        })
      },
    },
    onShow() {
      wx.setNavigationBarTitle({title: '订单详情页'})
    }
  }
</script>
<style scoped>
  .container{width:100%;height:100vh;background:#f5f5f5}
  .item{border-bottom: 1px solid #f5f5f5;padding: 8px 10px;}
  .item img{width: 80px;height: 60px;border-radius: 3px}
  .contactBtn{padding: 8px 0;border: 1px solid #eee;}
</style>
