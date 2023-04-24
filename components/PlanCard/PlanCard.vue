<template>
	<view class="item">
		<view class="time">
			<image src='../../static/ICON/92.png'></image>
			<text>{{info.time}}</text>
		</view>
		<view class="address">
			<image src='../../static/ICON/91.png'></image>
			<text>{{info.address}}</text>
		</view>
		<image :src='info.img' mode="aspectFill"></image>

		<view class="main">
			<view class="left">
				<view class="title">{{info.goodsname}}</view>
				<view class="price">￥{{info.price}}</view>
			</view>
			<view class="right">
				<view class="phone" @click='makeCall'>
					<image src='../../static/ICON/93.png'></image>
					<text>电话</text>
				</view>
				<view class="service">
					<image src='../../static/ICON/93.png'></image>
					<text>服务</text>
				</view>
			</view>
		</view>
		<view class="btn">
			<button>我的账单</button>
		</view>
	</view>
</template>

<script>
	export default {
		name: "PlanCard",
		props: ['info'],
		data() {
			return {
				// a:'1'
			};
		},
		methods: {
			makeCall() {
				console.log(this.info)
				let _that = this
				uni.showModal({
					title: this.info.pname,
					content: this.info.tel,
					confirmText: '拨打电话',
					cancelText: '取消',
					confirmColor: '#f80',
					success: function(res) {
						if (res.confirm) {
							//拨打电话了 
							uni.makePhoneCall({
								phoneNumber: _that.info.tel //仅为示例
							});
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					}
				});
			}
		},
	}
</script>

<style lang="less">
	.item {
		box-shadow: 0px 0px 10px rgba(100, 100, 100, 0.3);
		border-radius: 20rpx;
		position: relative;
		margin-bottom: 30rpx;
		padding-bottom: 30rpx;

		.time {
			padding: 28rpx;
			display: flex;
			align-items: center;

			image {
				width: 36rpx;
				height: 36rpx;
				margin-right: 12rpx;
			}
		}

		.address {
			padding: 0px 28rpx;
			display: flex;
			align-items: center;

			image {
				width: 36rpx;
				height: 36rpx;
				margin-right: 12rpx;
			}
		}

		image {
			margin-top: 20rpx;
			width: 100%;
			height: 400rpx;
		}

		;

		.main {
			display: flex;
			padding: 20rpx;
			justify-content: space-between;
			align-items: center;

			.left {
				.title {
					font-weight: bolder;
					font-size: 34rpx;
					letter-spacing: 4rpx;

				}

				.price {
					color: red;
				}
			}

			.right {
				display: flex;
				justify-content: center;
				align-items: center;

				.phone,
				.service {
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;

					image {
						width: 50rpx;
						height: 50rpx;
					}

					text {
						color: #F3A73F;
					}
				}

				.phone {
					margin-right: 50rpx;
				}



				text {
					color: #ccc;
				}
			}
		}

		.btn {
			width: 90%;
			margin: 0 auto;

			button {
				background-color: #fa491d;
				text-align: center;
				color: #FFFFFF;
				letter-spacing: 2rpx;
				// padding: 30rpx;
			}
		}
	}
</style>
