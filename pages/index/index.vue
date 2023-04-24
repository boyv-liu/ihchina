<template>
	<view class="content">
		<!-- 第一页 -->
		<view class="page-one">
			<view class="fixed-box">
				<!-- 导航 -->
				<view class="bar">
					<img src="@/static/logo.png" alt="">
					<view class="head">
						<text class="title">{{title}}</text>
						<!-- icons -->
						<view class="icons">
							<i class="iconfont icon-31sousuo"></i>
							<i class="iconfont icon-weixin">
								<img src="@/static/code.png" mode="center" style="width: 280rpx;height: 280rpx;" alt="">
							</i>
							<i class="iconfont icon-weibo"></i>
						</view>
						<text>{{showDate}}</text>
					</view>
				</view>
				<!-- tabs -->
				<view class="tab-box">
					<v-tabs v-model="activeMenu" :scroll="false" :tabs="tabs" @change="changeTab"></v-tabs>
				</view>
			</view>
			
			<!-- 轮播图 -->
			<uni-swiper-dot @clickItem="clickSwiper" class="swiper" :info="swiperInfo" :current="current" field="content" mode="round">
				<swiper class="swiper-box" @change="change" :autoplay="true" :circular="true" :current="current">
					<swiper-item v-for="(item ,index) in swiperInfo" :key="index">
						<view class="swiper-item" :class="'swiper-item' + index">
							<img mode="scaleToFill" :src="getSrc(index)" alt="" lazy-load draggable="false">
						</view>
					</swiper-item>
				</swiper>
			</uni-swiper-dot>
	
		</view>
		<!-- 第二页 -->
		<view class="page-two">
			<view class="lines">
				<img :src=" '/static/c' + item + '.png' " alt="" mode="scaleToFill" class="line" v-for="item in lines">
			</view>
			<view class="left">
				<view class="icon-img before-img"></view>
				<text class="title">国家级非物质文化遗产代表性项目名录</text>
				<view class="icon-img after-img"></view>
			</view>
			<!-- 项目明细 -->
			<view class="product">
				<view class="item" v-for="(item,index) in productList" :style="{'top': item.top, 'marginLeft': item.left, 'background': item.background,'backgroundSize': 'contain'}">
					<img :src=" '/static/b' + index + '-1.png' " alt="" >
					<view class="note">{{item.name}}</view>
				</view>
			</view>
		</view>
		<!-- 第三页 -->
		<view class="page-three">
			<view class="title-item">中国入选联合国教科文组织非物质文化遗产</view>
			<view class="title-item">名录（名册）项目</view>
			<view class="title-item">共计43项</view>
		</view>
		<!-- 第四页 -->
		<view class="page-four">
			<img src="/static/page4.png"  mode="scaleToFill" alt="" style="height: 100%;width: 100%;" >
		</view>
	</view>
</template>

<script>
	import solarlunar from 'solarlunar'

	export default {
		data() {
			return {
				title:'中国非物质文化遗产网·中国非物质文化遗产数字博物馆',
				showDate:'', // 日期
				activeMenu: 0,
				tabs: ['首页', '机构', '政策', '咨讯', '清单', '资源', '学术', '百科',], // tabs
				swiperInfo: [0,1,2],
				current: 0,
				lines:[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20], // 线条
				productList:[
					{name:'【 民间文学 】',top:'30%',left:'15%',background:'url("/static/b0.png") no-repeat top left'},
					{name:'【 传统音乐 】',top:'40%',left:'25%',background:'url("/static/b1.png") no-repeat top left'},
					{name:'【 传统舞蹈 】',top:'10%',left:'30%',background:'url("/static/b2.png") no-repeat top left'},
					{name:'【 传统戏剧 】',top:'20%',left:'40%',background:'url("/static/b3.png") no-repeat top left'},
					{name:'【 曲艺 】',top:'50%',left:'40%',background:'url("/static/b4.png") no-repeat top left'},
					{name:'【 传统体育、游艺与杂技 】',top:'30%',left:'50%',background:'url("/static/b5.png") no-repeat top left'},
					{name:'【 传统美术 】',top:'35%',left:'60%',background:'url("/static/b6.png") no-repeat top left'},
					{name:'【 传统技艺 】',top:'15%',left:'70%',background:'url("/static/b7.png") no-repeat top left'},
					{name:'【 传统医药 】',top:'45%',left:'75%',background:'url("/static/b8.png") no-repeat top left'},
					{name:'【 民俗 】',top:'35%',left:'85%',background:'url("/static/b9.png") no-repeat top left'},
				]
			}
		},
		onLoad() {},
		mounted() {
			// 日期
			this.getDate()
		},
		methods: {
			getDate(){
				const nowDate = new Date()
				const data = solarlunar.solar2lunar(nowDate.getFullYear(), nowDate.getMonth() + 1, nowDate.getDate())
				// console.log(data)
				if(data != -1){
					this.showDate = `${data.cYear}-${data.cMonth}-${data.cDay}　${data.ncWeek}　农历${data.monthCn}${data.dayCn}　${data.term} `
				}else{
					console.log('日期转化出错')
					this.showDate = ''
				}
			},
			// tab
			changeTab(index) {
			  console.log('当前选中的项：' + index)
			},
			
			// swiper 
			getSrc(index){
				return `static/swiper-${index+1}.jpeg`
			},
			change(e) {
				this.current = e.detail.current
			},
			clickSwiper(val){
				this.current = val
			}
		
		}
	}
</script>

<style lang="less" scoped>
	.content {
		width: 100%;
	}
	// 第一页
	.page-one{
		height: 100vh;
		position: relative;
		text{
			color: #fff;
		}
		.fixed-box{
			z-index: 99;
			width: 100%;
			position: absolute;
			top: 0;
			
			.bar{
				padding: 30rpx 120rpx;
				background-color: rgba(0, 0, 0,.2);
				display: flex;
				align-items: center;
				cursor: pointer;
				border-bottom: 1rpx solid #aaa;
				
				.head{
					z-index: 9999;
					font-size: 32rpx;
					margin-left: 32rpx;
					width:100%;
					display: flex;
					justify-content: space-between;
					align-items: center;
					.title{
						flex: 1;
					}
					.icons{
						position: relative;
						padding: 0 100rpx;
						i{
							font-size: 40rpx;
							margin-right: 60rpx;
						}
					}
					img{
						
						position: absolute;
						padding: 8rpx;
						display: none;
						top: 80rpx;
						width: 300rpx;
						height: 300rpx;
						background-color: #fff;
						border-radius: 15rpx;
					}
				}
				.icon-weixin:hover img{
					display: block;
				}
				
				
			}
			// tabs
			.tab-box{
				padding:0 500rpx;
				background-color: rgba(0, 0, 0,.2);
			}
		}
	
		// 轮播
		.swiper{
			height: 100%;
			.swiper-item{
				height: 100%;
				width: 100%;
			}
			.swiper-box{
				height: 100%;
				width: 100%;
				img{
					height: 100%;
					width: 100%;
				}
			}
		}
	}
	
	// 第二页
	.page-two{
		height: 100vh;
		position: relative;
		.lines{
			height: 100%;
			display: flex;
			.line{
				width: 5%;
			}
			
		}
		.left{
			.title{
				position: absolute;
				top: 18%;
				color: #fff;
				margin-left: 6.3%;
				writing-mode: vertical-rl;
				font-size: 60rpx;
			}
			.icon-img{
				position: absolute;
				margin-left: 6.3%;
				width: 70rpx;
				height: 80rpx;
			}
			.before-img{
				top: 12%;
				background: url('/static/kuohao.png') no-repeat top left;
			}
			.after-img{
				bottom: 12%;
				background: url('/static/kuohao.png') no-repeat top right;
			}
		}
		
		.product{
			.item{
				position: absolute;
				width: 10%;
				height: 500rpx;
				cursor: pointer;
				
				.note{
					width: 100%;
					color: #fff;
					margin-top: 80rpx;
					text-align: center;
					font-size: 38rpx;
				}
			}
		}
	}

	// 第三页
	.page-three{
		height: 100vh;
		background: url('/static/page3bg.jpeg') no-repeat left top;
		background-size: cover;
		padding-top: 300rpx;
		.title-item{
			text-align: center;
			padding: 10rpx;
			font-size: 66rpx;
			color: #fff;
		}
	}
	
	// 第四页
	.page-four{
		height: 100vh;
	}
</style>
