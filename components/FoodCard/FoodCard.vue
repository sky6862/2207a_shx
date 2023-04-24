<template>
	<view class="item">
		<image :src='info.img' mode="aspectFill"></image>
		<view class="fire">
			<image src='../../static/ICON/icon_fire.png'></image>
			<text @click='zhixing'>18888</text>
		</view>
		<view class="main">
			<view class="left">
				<view class="title">{{info.goodsname}}</view>
				<view class="price">￥{{info.price}}</view>
			</view>
			<view class="right" @click='cancelOne(info.id)'>
				<image src="../../static/ICON/footer2.png"></image>
				<text >取消收藏</text>
			</view>
		</view>
	</view>

</template>

<script>
	export default {
		name: "FoodCard",
		props:['info','fn'],
		data() {
			return {

			};
		},
		mounted(){
			console.log(this.item)
		},
		methods:{
			zhixing(){
				this.fn()
			},
			cancelOne(id){
				this.$emit('deleteOne',id)
			}
		}
	}
</script>

<style lang="less" scoped>
	.item {
		box-shadow: 0px 0px 10px rgba(100, 100, 100, 0.3);
		border-radius: 20rpx;
		position: relative;
		margin-bottom: 30rpx;
		image {
			width: 100%;
			height: 400rpx;
			border-radius: 20rpx 20rpx 0 0;
		}

		;

		.fire {
			background-color: #b1b1b1;
			border-radius: 12rpx;
			padding: 10rpx 16rpx;
			display: flex;
			justify-content: center;
			align-items: center;
			position: absolute;
			right: 20rpx;
			top: 320rpx;

			image {
				width: 24rpx;
				height: 24rpx;
				margin-right: 12rpx;
			}

			text {
				color: #fff;
			}
		}

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
				flex-direction: column;
				align-items: center;

				image {
					width: 40rpx;
					height: 40rpx;

				}

				text {
					color: #ccc;
				}
			}
		}
	}
</style>
