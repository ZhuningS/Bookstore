<template>
  <div class="container ub-box ub-col">
    <dl class="ub-box ub-ver z-padding-v-10-px" style="background:#fff;">
      <dd @click.stop="$openWin('/pages/citySelect/main')" class="z-padding-h-10-px ub-box ub-ver">
        <span class="z-font-size-14 z-color-666 z-margin-right-3-px">{{curCity}}</span>
         <i class="iconfont icon-xiangxiazhankai z-color-666 z-font-size-16"></i>
      </dd>
      <dd class="ub-flex-1 ub-box ub-ver">
        <div @click.stop="$openWin('/pages/search/main')" class="search ub-box ub-ver-v z-width-90-percent z-box-sizing-border">
          <i class="iconfont icon-sousuo z-color-666 z-font-size-16"></i>
          <span class="z-font-size-14 z-color-999 z-margin-left-8-px">请输入书名、分类或者作者...</span>
        </div>
      </dd>
    </dl>
    <SubTitle :top5='top5'></SubTitle>
    <SubTitle :top5='visit'></SubTitle>
    <scroll-view scroll-y style="height: calc(100vh - 50px);" scroll-top="0">
      <!--轮播图-->
      <div class="ub-box ub-ver z-bg-color-fff">
        <swiper class="swiper" indicator-dots="false" autoplay="false" interval="5000" duration="500">
          <block v-for="(item, idx) in imgUrls" :key="idx">
            <swiper-item>
              <image :src="item" class="z-width-100-percent" mode="widthFix"/>
            </swiper-item>
          </block>
        </swiper>
      </div>
      <!--图标分类入口-->
      <dl class="ub-box ub-wrap z-padding-v-5-px" style="background:#fff">
        <div class="icon-item ub-box ub-col ub-ver" :key="key" v-for="(idx, key) in iconMap">
          <dd @click.stop="$openWin('/pages/error/main')" class="icon ub-box ub-ver iconfont" :class="key" :style="{background: iconMap[key]['bk']}"></dd>
          <span class="z-padding-v-8-px z-font-size-12 z-color-333">{{iconMap[key]['title']}}</span> 
        </div>
      </dl>
      <!--商品列表-->
      <dl class="ub-box ub-col z-margin-top-6-px z-padding-all-8-px" style="background:#fff">
        <p class="z-width-100-percent ub-box ub-ver" style="border-bottom:1px solid #eee">
          <span class="z-font-size-12 z-color-888 z-lineHeight-36">—图书列表—</span>
        </p>
        <dd class="ub-box ub-col">
          <good v-for="(val, idx) in 7" :key="idx" :isLast="idx===6"></good>
        </dd>
      </dl>
    </scroll-view>
  </div>
</template>
<script>
  import good from "../../components/good.vue"
  export default {
    components: {good},
    computed: {
      curCity () {
        return this.$store.state.curCity
      }
    },
    data () {
      return {
        books: [],
        page: 0,
        more: true,
        tops: [],
        top5: ['今日Top5'],
        visit: ['图书榜'],
        imgUrls: [
          'https://img3.doubanio.com/view/ark_article_cover/retina/public/110136604.jpg?v=1553852504',
          'https://img3.doubanio.com/view/subject/m/public/s32295155.jpg',
          'https://img3.doubanio.com/view/subject/m/public/s30021282.jpg',
        ],
        iconMap: {
          'icon-caigou': {title: '人文社科', bk: '#EF8B3E'}, 
          'icon-shangpin': {title: '自然科学', bk: '#E4463B'},
          'icon-touchengkongyun': {title: '历史', bk: '#8B67E5'},
          'icon-daohang': {title: '哲学', bk: '#5DC7B0'},
          'icon-zitigui': {title: '古书', bk: '#F3AE42'}
        },
      }
    },
    methods: {
      async initAjax() {
        let ret = await this.$ajax({url: 'https://devapi.ynshuke.com/v1/banners'})
        console.log(ret)
      }
    },
    mounted() {
      // this.initAjax()
    },
    onPullDownRefresh() {
      console.log('onPullDownRefresh');
      setTimeout(() => {wx.stopPullDownRefresh()}, 600)
    }
  }
</script>
<style scoped>
  .container{width:100%;height:100vh;background:#e8e8e8;}
  .search{background: #f5f5f5;border-radius: 12px;padding: 5px 10px}
  .swiper{height: 120px;width: calc(100% - 16px)}
  .icon-item{width:20%;padding: 10px 13px 0 13px;box-sizing: border-box;}
  .icon{width: 38px;height: 38px;border-radius: 50%;color: #fff;font-size: 24px}
  .adv{border-right: 2px solid #eee}
  .adv img{width: 50px;height: 50px}
  .good{border-bottom: 1px solid #DDD8CE}
  .good img{width: 80px;height: 80px}
</style>
