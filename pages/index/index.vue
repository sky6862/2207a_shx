<template>
	<view class="main">
		<!-- 轮播图区域 -->
		<view class="banner">
			<swiper class="swiper" autoplay="true" interval="2000" duration="500" circular='true' @change='getIndex'>
				<swiper-item v-for='(item,index) in swiperImg' :key='index'>
					<image :src="item.url" mode="aspectFill"></image>
				</swiper-item>
			</swiper>
			<view class="dots">
				<!-- 如何获取当前正在播放的那张轮播图的索引值  通过文档找到了方法-->
				<text v-for='(item,index) in swiperImg' :key='index' :class='index===activeIndex?"active":""'></text>
			</view>
		</view>
		<!-- 搜索框区域 -->
		<view class="search" @click='goSearch'>
			<image src='../../static/ICON/3.png'></image>
			<text>搜美食,菜谱</text>
		</view>
		<!-- 选项Icon区域 -->
		<view class="icons">
			<view class='item'>
				<image src='../../static/ICON/5.png'></image>
				<text>餐宴</text>
			</view>
			<view class='item'>
				<image src='../../static/ICON/7.png'></image>
				<text>名厨</text>
			</view>
			<view class='item'>
				<image src='../../static/ICON/4.png'></image>
				<text>坝坝宴</text>
			</view>
			<view class='item'>
				<navigator url="/pages/Around/Around">
					<image src='../../static/ICON/6.png'></image>
					<text>餐饮周边</text>
				</navigator>
			</view>
		</view>
		<!-- 中间图片区域 -->
		<view class="img">
			<image src='../../static/ICON/8.png'></image>
		</view>
		<!-- 灰条 -->
		<view class='greyline'></view>
		<!-- 优选名厨区域 -->
		<view class="youxuan">
			<image src='../../static/ICON/9.png' mode='aspectFit'></image>
			<view class="list" >
				<CCard class="item" v-for='(item,index) in cooker' :key='index' :info ='item'/>
			</view>
			<view class="title">更多名厨</view>
		</view>
		<!-- 灰条 -->
		<view class='greyline'></view>
		<!-- 优选餐宴区域 -->
		<view class="meal">
			<image src='../../static/ICON/10.png' mode='aspectFit'></image>
			<scroll-view scroll-x="true" class='list'>
				<view class='item'>
					<image src='../../static/ICON/goods1.jpg'></image>
					<view class="title">盛夏海鲜家宴</view>
					<view class="price">￥4999/桌</view>
				</view>
				<view class='item'>
					<image src='../../static/ICON/goods2.jpg'></image>
					<view class="title">精品西式家宴</view>
					<view class="price">￥1299/桌</view>
				</view>
				<view class='item'>
					<image src='../../static/ICON/goods3.jpg'></image>
					<view class="title">必胜客披萨宴</view>
					<view class="price">￥199/桌</view>
				</view>
			</scroll-view>
			<view class="more">更多餐宴</view>
		</view>
		<!-- 灰条 -->
		<view class='greyline'></view>
		<!-- 页脚说明 -->
		<view class="footer">
			<view class="item">
				<image src='../../static/ICON/13.png'></image>
				<view class="text">
					<view>信用保障</view>
					<view>服务到位，时间准时</view>
				</view>
			</view>
			<view class="item">
				<image src='../../static/ICON/14.png'></image>
				<view class="text">
					<view>认证服务商</view>
					<view>厨师实名，服务更可靠</view>
				</view>
			</view>
			<view class="item">
				<image src='../../static/ICON/15.png'></image>
				<view class="text">
					<view>品质服务</view>
					<view>知名品牌，星级厨师</view>
				</view>
			</view>
			<view class="item">
				<image src='../../static/ICON/16.png'></image>
				<view class="text">
					<view>安全保障</view>
					<view>全平台在线支付</view>
				</view>
			</view>
		</view>
		<!-- 底部图片 -->
		<view class="bottem">
			<image src='../../static/ICON/gg.jpg'></image>
		</view>
	</view>
</template>

<script>
	import goodsJson from '../../static/goods-json.js'
	import CCard from '../../components/CookerCard/CookerCard.vue'
	export default {
		components:{
			CCard
		},
		data() {
			return {
				swiperImg: [{
					url: '../../static/ICON/goods1.jpg'
				}, {
					url: '../../static/ICON/goods2.jpg'
				}, {
					url: '../../static/ICON/goods3.jpg'
				}],
				activeIndex: 0,
				cooker: [],
			}
		},
		onLoad() {
			
		},
		mounted(){
			console.log(1)
			this.cooker=goodsJson.manlist
		},
		methods: {
			getIndex(e) { //获得当前播放的那张轮播图的索引值 current
				this.activeIndex = e.detail.current
			},
			goSearch() {
				uni.navigateTo({
					url: '../Search/Search'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.banner {
		position: relative;

		.swiper {
			height: 400rpx;

			image {
				width: 100%;

			}
		}

		.dots {
			position: absolute;
			left: 50%;
			transform: translateX(-50%);
			bottom: 80rpx;

			.active {
				width: 40rpx;
				background-color: #fff;
				border-radius: 10rpx;
			}

			text {
				display: inline-block;
				width: 20rpx;
				height: 20rpx;
				border-radius: 10rpx;
				background-color: #ccc;
				margin-right: 16rpx;
			}
		}
	}

	.search {
		width: 90%;
		margin: 0 auto;
		height: 100rpx;
		line-height: 100rpx;
		transform: translateY(-50%);
		background-color: white;
		border-radius: 60rpx;
		display: flex;
		justify-content: center;
		align-items: center;
		box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);

		image {
			width: 40rpx;
			height: 40rpx;
			margin-right: 20rpx;
		}

		text {
			color: #a8a8a8
		}
	}

	.icons {
		width: 90%;
		margin: 0 auto;
		padding: 0rpx 10rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;

		.item {
			image {
				width: 112rpx;
				height: 112rpx;
			}

			width: 150rpx;
			height: 220rpx;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
		}
	}

	.img {
		width: 90%;
		margin: 0 auto;

		image {
			width: 100%;
			height: 300rpx;
		}

		padding-bottom: 20rpx;
	}

	.greyline {
		height: 20rpx;
		background-color: #e1e1e1;
	}

	.youxuan {
		margin-top: 12rpx;
		text-align: center;
		padding-top: 20rpx;

		image {
			width: 500rpx;
			height: 80rpx;
		}

		.list {
			margin-top: 30rpx;
			display: flex;
			justify-content: space-around;

			.item {
				box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
				width: 220rpx;
				height: 280rpx;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;

				
			}
		}

		.title {
			color: #acacac;
			margin: 30rpx 0 30rpx;
			letter-spacing: 2rpx;
		}
	}

	.meal {
		margin-top: 12rpx;
		padding-top: 20rpx;

		image {
			width: 500rpx;
			height: 80rpx;
		}

		text-align: center;

		.list {
			margin-left: 20rpx;
			white-space: nowrap;
			margin-top: 20rpx;

			.item{
				text-align: start;
				display: inline-block;
				width: 300rpx;
				height: 330rpx;
				margin-right: 30rpx;
				border-radius: 20rpx;
				box-shadow: 1px 5px 5px rgba(0, 0, 0, 0.1);

				image {
					width: 300rpx;
					height: 200rpx;
					border-radius: 20px 20px 0px 0px;
				}

				;

				.title {
					font-weight: bolder;
					margin-top: 10rpx;
				}

				.price {
					color: red;
					margin: 10rpx 0;
				}
			}
		}

		.more {
			color: #acacac;
			margin: 30rpx 0 30rpx;
			letter-spacing: 2rpx;
		}
	}

	.footer {
		display: flex;
		flex-wrap: wrap;

		.item {
			&:nth-child(4) {
				padding-right: 50rpx;
			}

			&:nth-child(1),
			&:nth-child(3) {
				border-right: 1px solid #ebebeb;
				border-bottom: 1px solid #ebebeb;
			}

			&:nth-child(4),
			&:nth-child(2) {
				border-bottom: 1px solid #ebebeb;
			}

			width: 50%;
			height: 160rpx;
			display: flex;
			justify-content: center;
			align-items: center;

			image {
				width: 60rpx;
				height: 60rpx;
				margin-right: 20rpx;
			}

			.text {
				view:nth-child(1) {
					font-size: 26rpx;
				}

				view:nth-child(2) {
					font-size: 18rpx;
					color: #999999;
				}
			}
		}
	}

	.bottem {
		margin: 20rpx 0;

		image {
			width: 100%;
			height: 400rpx;
		}
	}
</style>
