<template>
  <div class="container ub-box ub-col ub-ver">
	<scroll-view scroll-y style="height: 100vh" scroll-top="0">
	  <dl class="ub-box ub-col">
		<dd class="z-width-100-percent z-box-sizing-border z-bg-color-fff">
			<image @click.stop="previewImage([indexImg])" class="z-width-100-percent z-img-cover indexImg" :src="indexImg">
				<div class="indexImg-bk ub-box ub-col">
					<span class="z-font-size-18 z-lineHeight-30 z-color-fff z-box-sizing-border z-padding-h-8-px">{{mainTitle}}</span>
					<span class="z-font-size-14 z-color-fff z-box-sizing-border z-padding-h-8-px">{{subTitle}}</span>
				</div>
			</image>
		</dd>
		<dd class="z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-between" style="border-bottom: 1px solid #f5f5f5">
			<p class="ub-box ub-ver">
				<span class="z-font-size-24 z-margin-right-5-px" style="color:#c11c06">¥{{nowPrice}}</span>
			</p>
			<p class="ub-box ub-ver">
				<span @click.stop="$openWin('/pages/submit/main')" class="buyBtn ub-box ub-ver z-font-size-16 z-color-fff">
					立即下单
				</span>
			</p>
		</dd>
		<dd class="z-margin-top-8-px z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-between" style="border-bottom: 1px solid #f5f5f5">
			<p class="ub-box ub-ver">
				<span class="z-font-size-13 z-color-888">
					<star></star>
				</span>
			</p>
			<p @click.stop="$openWin('/pages/comment/main')" class="ub-box ub-ver">
				<span class="z-font-size-13 z-color-888">{{commentsNum}}条评论</span>
				<i class="iconfont icon-xiayiyeqianjinchakangengduo z-font-size-12 z-color-888"></i>
			</p>
		</dd>
		<dd class="z-width-100-percent z-box-sizing-border z-bg-color-fff  ub-box ub-wrap" style="padding:12px 8px 8px 8px">
			<span v-for="(val, idx) in labels" :key="idx" class="label z-font-size-13" :class="{'tuijian': val.type==1, 'butuijian': val.type==0}">{{val.name}} {{val.num}}</span>
		</dd>
		<dd class="z-margin-top-8-px z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-between" style="border-bottom: 1px solid #f5f5f5">
			<p class="z-font-size-14 z-color-888">商家信息</p>
		</dd>	
		<dd class="z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-between">
			<p class="ub-flex-1 ub-box ub-col" style="border-right: 1px solid #eee">
				<span class="z-font-size-14 z-lineHeight-24 z-color-333">{{sellerName}}</span>
				<span class="z-font-size-13 z-color-999">{{sellAdress}}</span>
			</p>
			<p @click.stop="clickCall()" class="ub-box ub-ver z-padding-h-8-px">
				<i class="iconfont icon-dianhua z-font-size-20" style="color:#c11c06"></i>
			</p>
		</dd>
		</dd>
		<dd class="z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-ver" style="border-bottom: 1px solid #f5f5f5">
			<p class="z-font-size-14 z-color-888">备注</p>
		</dd>
		<dd class="z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-col">
			<ul class="ub-box ub-col">
				<li v-for="(val, idx) in package.notes" :key="idx" class="z-font-size-14 z-color-333 z-box-sizing-border z-lineHeight-24">{{val}}</li>
			</ul>
		</dd>
		<dd class="z-margin-top-8-px z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-between" style="border-bottom: 1px solid #f5f5f5">
			<p class="ub-box ub-ver">
				<span class="z-font-size-14 z-color-888">
					<star></star>
				</span>
			</p>
			<p @click.stop="$openWin('/pages/comment/main')" class="ub-box ub-ver">
				<i class="iconfont icon-xiayiyeqianjinchakangengduo z-font-size-12 z-color-888"></i>
			</p>
		</dd>
		<dd class="z-box-sizing-border z-bg-color-fff z-padding-all-8-px ub-box ub-between">
			<ul class="ub-flex-1 ub-box ub-col">
				<li v-for="(val, idx) in comments" :key="idx" class="z-border-bottom-1-eee">
					<comment :comment="val" :isShowLike="false"></comment>
				</li>
			</ul>
		</dd>
		<dd @click.stop="$openWin('/pages/comment/main')" class="z-width-100-percent z-box-sizing-border z-bg-color-fff z-padding-h-8-px ub-box ub-between">
			<p class="z-margin-bottom-8-px ub-box ub-ver">
				<span style="color:#c11c06" class="z-font-size-14 z-color-888">查看全部评价</span>
			</p>
			<p class="ub-box ub-ver">
				<i class="iconfont icon-xiayiyeqianjinchakangengduo z-font-size-13 z-color-888"></i>
			</p>
		</dd>
	  </dl>
	</scroll-view>
  </div>
</template>
<script>
	import good from "../../components/good.vue"
	import star from "../../components/star.vue"
	import comment from "../../components/comment.vue"
	export default {
		components: {good, star, comment},
	  	data () {
			return {
				indexImg: 'https://img3.doubanio.com/lpic/s29509182.jpg',
				mainTitle: '时间简史',
				subTitle: '精装版',
				nowPrice: '38',
				normalPrice: '398',
				labels: [
					{name: '棒', num: '202', type: '1'}, 
					{name: '好', num: '97', type: '1'},
					{name: '很好', num: '40', type: '1'}, 
					{name: '不错', num: '22', type: '1'},
					{name: '不推荐', num: '29', type: '0'},
					{name: '还可以', num: '13', type: '0'},
					{name: '朋友推荐', num: '9', type: '0'}, 
					{name: '不好', num: '5', type: '0'},
					{name: '还行', num: '4', type: '0'}, 
					{name: '可以的', num: '4', type: '0'},
				],
				sellerName: '科技教育书店',
				sellAdress: '市区南路777号49楼',
				package: {
					packageName: '时间简史',
					notes: [
						'励志格言：知识就是力量。',
					],
				},
				purchaseInfo: {
					validityDate: '2016.2.5 至 2018.6.14',
					unavailableDate: '周五至周日',
					rules: [
						'励志格言：知识就是力量。',
					]
				},
				commentsNum: 6,
				comments: [
					{
						header: 'https://img3.doubanio.com/lpic/s29509182.jpg',
						name: 'AqU753874254',
						time: '2019-05-07', 
						star: '4.0',
						say: '超级棒！很满意 ', 
						imgs: [
							'https://img1.doubanio.com/view/subject/m/public/s32288967.jpg'							
						]
					},
					{
						header: 'https://img1.doubanio.com/view/subject/m/public/s32288967.jpg',
						name: 'PPL546030823',
						time: '2019-05-06', 
						star: '4.5',
						say: '很好', 
						imgs: [
							'https://img1.doubanio.com/view/subject/m/public/s32288967.jpg',
							'https://img3.doubanio.com/view/subject/m/public/s32299536.jpg',
							'https://img3.doubanio.com/view/ark_article_cover/retina/public/114707416.jpg?v=1557219220',

						]
					},
				],
			}
		},
		methods: {
			previewImage(imgs=[], curIdx=0){
				wx.previewImage({current: imgs[curIdx], urls: imgs})
			},
			clickCall() {
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
    		wx.setNavigationBarTitle({title: this.mainTitle})
  		}
	}
</script>
<style scoped>
  .container{width:100%;height:100vh;background:#e8e8e8}
  .indexImg{height: 170px;position: relative;}
  .indexImg-bk{position: absolute;bottom: 0;left: 0;z-index: 1;width: 100%;height: 30%;background: rgba(0,0,0,.3);padding: 5px 0px}
  .buyBtn{background: #f90;padding: 8px 12px;border-radius:3px}
  .label{border-radius:3px;background: #fff;padding: 3px 5px;margin: 0 5px 5px 0}
  .tuijian{color: #f90;border:1px solid #f90;}
  .butuijian{color: #999;border:1px solid #ddd;}
</style>
