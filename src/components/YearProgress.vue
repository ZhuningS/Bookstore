<template>
    <div class="progressbar">
       <p>小贴士</p>
       <progress percent="92.1"  activeColor="#009999" backgroundColor="red"/>
       <p>{{year}}年已经过去了<span class="key">{{days}}</span>天,<span class="key">{{percent}}%</span></p>
    </div>
</template>


<script>
export default {
  methods: {
    // 判断是闰年还是其他
    isLeapYear () {
      const year = new Date().getFullYear()
      if (year % 400 === 0) {
        return true
      } else if (year % 4 === 0 && year % 100 !== 0) {
        return true
      } else {
        return false
      }
    },
    // 获取多少天
    getDayOfYear () {
      return this.isLeapYear() ? 366 : 365
    }
  },
  computed: {
    year () {
      return new Date().getFullYear()
    },
    days () {
      let start = new Date()
      // start是今年第一天
      start.setMonth(0)
      start.setDate(1)
      // 用今天的时间戳减去今年第一天的时间戳
      let offset = new Date().getTime() - start.getTime()
      return parseInt(offset / 1000 / 60 / 60 / 24) + 1
    },
    percent () {
      return (this.days * 100 / this.getDayOfYear()).toFixed(1)
    }
  }
}
</script>

<style lang="less">
    .progressbar{
        color:dimgray;
        width: 98%;
        text-align: center;
        background-color:whitesmoke;
        margin: 30rpx auto;
        border-radius: 10%;
        progress{
            margin-top: 20rpx;
            margin-bottom: 20rpx;
        }
        p{
            .key{
                color:tomato;
            }
        }
    }
</style>


