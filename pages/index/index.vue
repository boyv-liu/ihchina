<template>
	<view class="content">
		<!-- 第一页 -->
		
		<view class="page-one">
			<view class="bar">
				<img src="../../static/logo.png" alt="">
				<text class="title">{{title}}</text>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:'中国非物质文化遗产网·中国非物质文化遗产数字博物馆',
				
			}
		},
		onLoad() {},
		methods: {

		}
	}
</script>

<style lang="less" scoped>
	.content {
		width: 100%;
	}
	// 第一页
	.page-one{
		.bar{
			padding: 10rpx 50rpx;
			width: 100%;
			color: #fff;
			background-color: rgba(179, 184, 188, .8);
			display: flex;
			align-items: center;
			
			.title{
				font-size: 14rpx;
				margin-left: 16rpx;
			}
		}
	}
	
</style>
