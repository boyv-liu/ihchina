<template>
	<view class="content">
		<full-page :options="options">
			<!-- 第一页 -->
			<div class="section">
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
				
			</div>
			<!-- 第二页 -->
			<div class="section">
			   <view class="page-two">
				<view class="lines">
					<img :src=" '/static/c' + item + '.png' " alt="" mode="scaleToFill" class="line" v-for="item in lines">
				</view>
				<view class="head-title">
					<view class="icon-img before-img"></view>
					<text class="title">国家级非物质文化遗产代表性项目名录</text>
					<view class="icon-img after-img"></view>
				</view>
				<!-- 项目明细 -->
				<view class="product">
					<view class="item" @click="toDetail(index)" v-for="(item,index) in productList" :style="{'top': item.top, 'marginLeft': item.left, 'background': item.background,'backgroundSize': 'contain'}">
						<img :src=" '/static/b' + index + '-1.png' " alt="" >
						<view class="note">{{item.name}}</view>
					</view>
				</view>
			   </view>   
			</div>
			<!-- 第三页 -->
			<div class="section">
				<view class="page-three">
					<view class="title-item">中国入选联合国教科文组织非物质文化遗产</view>
					<view class="title-item">名录（名册）项目</view>
					<view class="title-item">共计43项</view>
				</view>
			</div>
			<!-- 第四页 -->
			<div class="section">
				<view class="page-four">
					<img src="/static/page4.png"  mode="scaleToFill" alt="" style="height: 100%;width: 100%;" >
				</view>
			</div>
			<!-- 第五页 -->
			<div class="section">
				<view class="page-five">
					<view class="head-title">
						<view class="icon-img-row left-img"></view>
						<text class="title">非物质文化遗产地图</text>
						<view class="icon-img-row right-img"></view>
					</view>
					<view class="bottom">
						<view class="china-map" id="china-map" style="width: 850px;height: 641px;" ref="charts"></view>
						<img style="width: 800rpx;height: 1000rpx;" src="/static/page5info.png" alt="">
					</view>
					
				</view>
			</div>
			<!-- 第六页 -->
			<div class="section">
				<view class="page-six">
					<image :src="'/static/page6-'+index+'.jpeg'" alt="" v-show="active == index"  v-for="(item,index) in characterList"  mode="aspectFill" style="width: 60%;height: 100%;"></image>
					<view class="right-liens">
						<view class="title">人物</view>
						<view class="line"  v-for="(item,index) in characterList" @mouseenter="active = index" @mouseout="active = index">
							<a :href="item.link" target="_blank">{{item.name}}</a>
						</view>
					</view>
				</view>
			</div>
			<!-- 第七页 -->
			<div class="section">
				<view class="page-seven">	
					<img src="/static/page7-left.png"  alt="" :class="{'left':true,'moveBottom':showAnimation,'moveTop':!showAnimation}" />
					<img src="/static/page7-right.png" alt="" :class="{'right':true,'moveBottom':!showAnimation,'moveTop':showAnimation}">
					<view class="left-info info">
						<view class="title">传统工艺振兴计划</view>
						<view>
							为落实党的十八届五中全会关于“构建中华优秀传统文化传承体系，加强文化遗产保护，振兴传统工艺”和《中华人民共和国国民经济和社会发展第十三个五年规划纲要》关于“制定实施中国传统工艺振兴计划”的要求，促进中国传统工艺的传承与振兴，文化部、工业和信息化部、财政部联合制定了《中国传统工艺振兴计划》，于2017年3月正式出台。
						</view>
						<a href="https://www.ihchina.cn/rejuvenation.html" target="_blank">查看更多</a>
					</view>
					<view class="right-info info">
						<view class="title">中国非物质文化遗产传承人研修培训计划</view>
						<view>
							自2015年“中国非物质文化遗产传承人群研修研习培训计划”实施以来，完成了“十三五”培训传承人群10万人次的目标任务，形成了较为明确的教学体系、工作规范和管理方式，有效调动了院校参与非物质文化遗产（以下简称“非遗”）保护工作，为非遗保护引入了重要力量；扩大了非遗传承人才队伍，促进了非遗保护理念的社会传播；提高了传统工艺设计制作水平，改善了一批项目保护传承情况；拓展了非遗保护传承的手段和方式，推动了一批示范性项目和探索性项目。同时，在振兴传统工艺、促进曲艺传承发展、助力脱贫攻坚等方面发挥了积极作用，社会影响力不断增强。“中国非物质文化遗产传承人群研修研习培训计划”已经成为非遗保护事业的一项基础性、战略性工作。
						</view>
						<a href="https://www.ihchina.cn/train.html" target="_blank">查看更多</a>
					</view>
				</view>
			</div>
			<!-- 第八页 -->
			<div class="section">
				<view class="page-eight">	
					<view class="left">
						<img @click="toMore" src="/static/page8-title.png" style="width: 40%;height: 70%;margin-top: 70%;" alt="">
					</view>
					<view class="accordion">
						<view class="item" v-for="(item,index) in accordionList" @mouseenter="handleEnter(index)" @mouseout="handleOut(index)" :style="{'background':item.background,'flex':item.isHover}">
							<a :href="item.link" target="_blank">{{item.name}}</a> 
						</view>
					</view>
				</view>
			</div>
			<!-- 第九页 -->
			<div class="section">
				<view class="page-nine">
					<img src="/static/page9bg.png"  mode="scaleToFill" alt="" style="height: 100%;width: 100%;" >
				</view>
			</div>
		</full-page>
	</view>
</template>

<script>
	import solarlunar from 'solarlunar'
	import * as echarts from "echarts"
	import chinaMap from '@/static/map/china-area.json'


	export default {
		data() {
			return {
				options: {
					licenseKey: "OPEN-SOURCE-GPLV3-LICENSE",
					//是否显示导航，默认为false
					navigation: true,
					//为每个section设置背景色
					sectionsColor: [],
					onLeave:this.pageLeave,
				},
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
				],
				characterList:[
					{name:'张树萍：初心不改，戏大于天',link:'https://www.ihchina.cn/character_detail/8578.html'},
					{name:'刘兰芳：从艺60周年回眸',link:'https://www.ihchina.cn/character_detail/18817.html'},
					{name:'刘魁立：行走田野 问俗追风',link:'https://www.ihchina.cn/character_detail/18671.html'},
					{name:'姚惠芬：走进威尼斯双年展的中国苏绣大师',link:'https://www.ihchina.cn/character_detail/8649.html'},
					{name:'尚长荣：“老戏骨”的创新之路',link:'https://www.ihchina.cn/character_detail/8661.html'},
					{name:'刘锡诚：心无旁骛的民间文学守望者',link:'https://www.ihchina.cn/character_detail/8724.html'},
				],
				active:0, // page6图片的显示
				showAnimation:false, // page7的动画显示
				accordionList:[
					{name:'宣纸传统制作技艺',link:'https://www.ihchina.cn/page_special.html',isHover:1,background:'url("/static/page8-0.jpeg") no-repeat center left 20%',link:'https://www.ihchina.cn/page_special.html'},
					{name:'二十四节气',link:'https://www.ihchina.cn/solar_terms.html',isHover:3,background:'url("/static/page8-1.jpeg") no-repeat center left 20%',link:'https://www.ihchina.cn/solar_terms.html'},
					{name:'太极拳',link:'https://www.ihchina.cn/tjq_home.html',isHover:1,background:'url("/static/page8-2.jpeg") no-repeat center left 20%',link:'https://www.ihchina.cn/tjq_home.html'},
					{name:'文化和自然遗产日',link:'https://www.ihchina.cn/special2022.html',isHover:1,background:'url("/static/page8-3.jpeg") no-repeat center left 20%',link:'https://www.ihchina.cn/special2022.html'},
					{name:'影音',link:'https://www.ihchina.cn/video.html',isHover:1,background:'url("/static/page8-4.jpeg") no-repeat center left 20%',link:'https://www.ihchina.cn/video.html'},
				]
			}
		},
		onLoad() {},
		mounted() {
			// 日期
			this.getDate()
			// 地图
			this.initMap()
		},
		methods: {
			// 日期
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
			// 代表
			toDetail(index){
				let url = 'https://www.ihchina.cn/project.html?tid=' + Number(index+1) +  '#sy_target1'
				window.open(url)
			},
			// page滚动
			pageLeave(index, nextIndex, direction){
				// console.log(nextIndex.index)
				if(nextIndex.index == 6){
					// 加载动画
					this.showAnimation = true
				}else{
					this.showAnimation = false
				}
			},
			// 地图
			initMap(){
				// const charts = echarts.init(this.$refs["charts"])
				var charts = echarts.init(document.getElementById('china-map'));
				const option = {
					// 背景颜色
					// backgroundColor: "rgba(128, 128, 128, 0)",
					// 提示浮窗样式
					tooltip: {
						show: true,
						trigger: 'item', //坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用
						// axisPointer: {// 坐标轴指示器，坐标轴触发有效
						//     type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
						// },
						alwaysShowContent: false,
						backgroundColor: "#b0a18a",
						borderColor: "#b0a18a",
						triggerOn: "mousemove",
						enterable: true, //鼠标是否可进入提示框浮层中
						textStyle: {
							fontSize: "12",
							overflow: "break",
							color: "#fff",
						},
						formatter: function (params) {
							let str = '';
							str = `<div> ` + params.name + `:` + params.value + `</div>`                   
							return str
						},
					},
					// 地图配置
					geo: {
						map: "china",
						zoom: 1.8, //视觉比例大小,1.2即为原有大小的1.2倍
						roam: false, //是否开启鼠标缩放和平移漫游。默认不开启。可以不用设置,如果只想要开启缩放或者平移，可以设置成 'scale' 或者 'move'。
						top: '30%',
						left:'25%',
						label: {
							// 通常状态下的样式
							normal: {
								show: true,
								textStyle: {
									color: "#fff",
								},
								fontSize: '9'
							},
							// 鼠标放上去的样式
							emphasis: {
								textStyle: {
									color: "#fff",
								},
							},
						},
						// 地图区域的样式设置
						itemStyle: {
							normal: {
								areaColor: "rgba(128, 128, 128, 0)",
								borderColor: "#887d6a",
								borderWidth: 0,
							},
							
							// 鼠标放上去高亮的样式
							emphasis: {
								areaColor: "rgba(128, 128, 128, 0)",
								borderWidth: 0,
							},
						},
					},
				}
				echarts.registerMap("china", chinaMap )
				charts.setOption(option)
			},
			// tab
			changeTab(index) {
			  console.log('当前选中的项：' + index)
			  switch(index){
				case 1:
					window.open('https://www.ihchina.cn/jigou')
				break
				case 2:
					window.open('https://www.ihchina.cn/zhengce')
				break
				case 3:
					window.open('https://www.ihchina.cn/zixun')
				break
				case 4:
					window.open('https://www.ihchina.cn/project.html')
				break
				case 5:
					window.open('https://www.ihchina.cn/ziyuan')
				break
				case 6:
					window.open('https://www.ihchina.cn/xueshu')
				break
				case 7:
					window.open('https://www.ihchina.cn/shenbaozhinan.html')
				break
			  }
			  
			  
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
			},
			// 查看更多
			toMore(){
				window.open('https://www.ihchina.cn/zhanlan.html')
			},
			// 手风琴
			handleEnter(index){
				this.accordionList.forEach((item,i)=>{
					if(index == i){
						item.isHover = 3
					}else{
						item.isHover = 1
					}
				})
			},
			handleOut(index){
				this.accordionList.forEach((item,i)=>{
					item.isHover = 1
				})
			},
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
		// 标题
		.head-title{
			.title{
				position: absolute;
				top: 18%;
				color: #fff;
				margin-left: 6.3%;
				font-size: 60rpx;
				writing-mode: vertical-rl;
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
		background: url('/static/page3bg.jpeg') no-repeat right top;
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
	
	// 第五页
	.page-five{
		position: relative;
		padding: 4% 6% 2% 6%;
		box-sizing: border-box;
		height: 100vh;
		view{
			color: #fff;
		}
		background: url('/static/page5bg.jpeg') no-repeat top right;
		
		// 地图
		.china-map{
			background: url('/static/map.png') no-repeat;
		}
		// 标题
		.head-title{
			text-align: center;
			position: relative;
			font-size: 60rpx;
			padding-bottom: 20rpx;
			.icon-img-row{
				position: absolute;
				width: 45rpx;
				height: 70rpx;
			}
			.left-img{
				left: 32%;
				background: url('/static/kuohaorow.png') no-repeat top left;
			}
			.right-img{
				right: 32%;
				top: 0;
				background: url('/static/kuohaorow.png') no-repeat top right;
			}
		}
		
		.bottom{
			height: 80vh;
			display: flex;
			align-items: center;
			justify-content: space-between;
		}
		
	}
	
	// 第六页
	.page-six{
		display: flex;
		height: 100vh;
		box-sizing: border-box;
		background: url('/static/page6bg.jpeg') no-repeat top right 40%;
		background-size: cover;

		.right-liens{
			width: 40%;
			height: 100%;
			padding: 0 150rpx;
			display: flex;
			align-items: center;
			
			.title{
				position: relative;
				font-size: 60rpx;
				padding: 0 100rpx;
				writing-mode: vertical-rl;
				
				&:before{
					content: '';
					position: absolute;
					top: -100rpx;
					display: block;
					width: 70rpx;
					height: 80rpx;
					background: url('/static/kuahaoblack.png') no-repeat ;
				}
				&:after{
					content: '';
					position: absolute;
					bottom: -120rpx;
					left: 96rpx;
					display: block;
					width: 70rpx;
					height: 80rpx;
					background: url('/static/kuahaoblack.png') no-repeat top right;
				}
			}
		
			.line{
				height: 100%;
				padding: 0 30rpx;
				writing-mode: vertical-rl;
				position: relative;
				cursor: pointer;
				
				&:before{
					content: '';
					position: absolute;
					right: 50%;
					top: 0;
					bottom: 0;
					border-left: 1px solid #ccc;
				}
				&:hover a{
					color: #f66;
				}
				&:hover &:before{
					border-left: 1px solid #f66;
				}
					
				a{
					position: relative;
					display: inline-block;
					padding: 30rpx 0;
					top: 20%;
					background: url('/static/page6line.png') no-repeat;
					background-size: cover;
				}
				
				&:nth-child(odd) a{
					top: 40%;
				}
				
			}
			
		}
	}
	
	// 第七页
	.page-seven{
		height: 100vh;
		position: relative;
		background: url('/static/page7bg.jpeg') no-repeat top left;
		overflow: hidden;
		.left{
			position: relative;
			width: 70%;
			height: 60vh;
			left: -6%;
			top: -55vh;
		}
		.moveBottom{
			transition: all 2s linear;
			transform: translate(0,55vh);
		}
		.moveTop{
			transition: all 2s linear;
			transform: translate(0,-55vh);
		}
		.right{
			position: absolute;
			right: -15%;
			bottom: -55vh;
		}
		.info{
			position: absolute;
			width: 40%;
			.title{
				text-indent: .5rem;
				font-size: 50rpx;
				padding-bottom: 50rpx;
			}
			view{
				text-indent: .5rem;
				color: #fff;
				line-height: 45rpx;
			}
			a{
				display: inline-block;
				padding-top: 50rpx;
				color: #fff;
			}
			
		}
		.left-info{
			left: 100rpx;
		}
		.right-info{
			right: 100rpx;
			top: 400rpx;
		}
	
	}
	
	// 第八页
	.page-eight{
		height: 100vh;
		display: flex;
		.left{
			text-align: center;
			width: 16%;
			// height: 100vh;
			background: url('/static/page8-left.jpeg') no-repeat center;
			img:hover{
				cursor: pointer;
			}
		}
		.accordion{
			flex: 1;
			display: flex;
			.item{
				writing-mode: vertical-lr;
				background-size: cover;
				// flex: 1;
				height: 100%;
				padding-left: 50rpx;
				text-align: center;
				a{
					font-size: 50rpx;
					color: #fff;
				}
				&:hover{
					cursor: pointer;
				}
				transition: all .5s linear;
			}
		}
		
	}
	
	// 第九页
	.page-nine{
		height: 100vh;
	}
	
	a{
		color: #333;
		border-bottom: 0;
		text-decoration: none;
	}
</style>
