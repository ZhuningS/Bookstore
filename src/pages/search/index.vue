<template>
  <div class="container">
    <dl class="ub-box ub-col">
      <dd class="z-width-100-percent z-padding-all-8-px z-bg-color-fff ub-box ub-ver z-box-sizing-border" style="80px;">
        <div class="ub-flex-1 search ub-box ub-ver-v">
          <i class="iconfont icon-sousuo z-color-666 z-font-size-16"></i>
          <input @input="doInput" @confirm="doSearch" class="ub-flex-1 z-font-size-14 z-color-666 z-padding-v-5-px z-margin-left-8-px" placeholder="C语言程序设计"/>
        </div>
        <span @click.stop="$backBeaforWin()" class="z-font-size-13 z-margin-left-8-px" style="color:#c11c06">取消</span>
      </dd>
      <!--搜索值不为空的时候，显示搜索列表-->
      <div v-if="searchVal.length>0" class="ub-box ub-col" style="padding:8px 8px 0 8px">
        <scroll-view scroll-y style="height: calc(100vh - 80px)" scroll-top="0">
          <ul class="ub-box ub-col">
            <li @click.stop="clickSearchItem(val)" v-if="currSearchList.length>0" class="search-item ub-box ub-ver z-box-sizing-border" v-for="(val, i) in currSearchList" :key="i">
              <i class="iconfont icon-sousuo z-color-999 z-font-size-16 z-margin-right-10-px"></i>
              <p class="ub-flex-1 z-color-333 z-font-size-14">{{val.val}}</p>
              <span class="z-font-size-12 z-color-999">总共{{val.num}}个结果</span>
            </li>
            <li @click.stop="clickSearchItem(searchVal)" v-if="currSearchList.length===0" class="search-item ub-box ub-ver z-box-sizing-border">
              <i class="iconfont icon-sousuo z-color-999 z-font-size-16 z-margin-right-10-px"></i>
              <p class="ub-flex-1 z-color-333 z-font-size-14">搜索"{{searchVal}}"</p>
              <i class="iconfont icon-xiayiyeqianjinchakangengduo z-color-999 z-font-size-16"></i>
            </li>
          </ul>
         </scroll-view>
      </div>
      <!--搜索值为空的时候，显示猜你想找和历史搜索-->
      <div v-if="searchVal.length===0" class="ub-box ub-col">
        <dd class="z-margin-h-8-px z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box">
          <ul class="ub-box ub-wrap">
            <li @click.stop="clickSearchItem(val)" v-for="(val, idx) in guess" :key="idx" class="item z-font-size-13 z-color-333">{{val.name}}</li>
          </ul>
        </dd>
        <dd class="z-margin-h-8-px z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-between">
          <p class="z-font-size-14 z-color-888">历史搜索</p>
          <i class="iconfont icon-juqianshou z-color-999 z-font-size-16"></i>
        </dd>
        <dd class="z-margin-h-8-px z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box">
          <ul class="ub-box ub-wrap">
            <li @click.stop="clickSearchItem(val)" v-for="(val, idx) in history" :key="idx" class="item z-font-size-13 z-color-333">{{val.name}}</li>
          </ul>
        </dd>
      </div>
    </dl>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        searchVal: '',
        // 测试搜索结果集
        searchAllList: [
          {id: '1', val: '时间简史', num: '7'},
          {id: '2', val: '时间简史2', num: '5'},
          {id: '3', val: '时间简史3', num: '3'},
          {id: '4', val: '时间简史4', num: '1'},
          {id: '5', val: '时间简史5', num: '1'},
          {id: '6', val: '时间简史6', num: '2'},
          {id: '7', val: '时间简史', num: '3'},
          {id: '8', val: '时间简史', num: '1'},
          {id: '9', val: '时间简史', num: '2'},
          {id: '10', val: '时间简史', num: '1'},
          {id: '11', val: '时间简史', num: '1'},
          {id: '12', val: '时间简史', num: '1'},
        ],
        currSearchList: [], // 当前根据搜索关键词搜索到的列表
        guess: [
          {goodId: '1', name: '时间简史'}, {goodId: '2', name: '时间简史'},
          {goodId: '3', name: '时间简史'}, {goodId: '4', name: '时间简史'},
          {goodId: '5', name: '时间简史'}, {goodId: '6', name: '时间简史'},
        ],
        history: [
          {goodId: '6', name: '时间简史'},
          {goodId: '3', name: '时间简史'},
        ]
      }
    },
    methods: {
      doInput(e) {
        this.searchVal = e.mp.detail.value
        this.filterList()
      },
      doSearch(e) {
        this.searchVal = e.mp.detail.value
      },
      filterList() {
        this.currSearchList = this.searchAllList.filter(item => {
          if (item.val.indexOf(this.searchVal) >= 0) return item
        })
      },
      clickSearchItem(val) {
        this.$redirectTo('/pages/error/main')
      },
    },
    mounted() {
      this.searchVal = ''
      this.currSearchList = JSON.parse(JSON.stringify(this.searchAllList))
    },
    onShow() {
      wx.setNavigationBarTitle({title: '搜索'})
    }
  }
</script>
<style scoped>
  .container{width:100%;height:100vh;background:#fff}
  .search{background: #f5f5f5;border-radius: 15px;padding: 0 10px}
  .search-item{border-bottom: 1px solid #eee;padding: 15px 0px;}
  .item{padding: 8px 10px;background: #f5f5f5;border-radius: 3px;margin: 0 8px 8px 0}
</style>
