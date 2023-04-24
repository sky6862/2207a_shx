<template>
	<view>
		<view class="pinfo">
			<view class="pname">
				<text>{{info.nickName}}</text>
				<text>欢迎您光临四海香</text>
			</view>
			<image :src='info.avatarUrl'></image>
		</view>
		<view class="list">
			<view class="item">
				<image src='../../static/ICON/icon_order.png'></image>
				<view class="right">
					<text>烹饪历史</text>
					<text>></text>
				</view>
			</view>
			<view class="item">
				<image src='../../static/ICON/icon_money.png'></image>
				<view class="right">
					<text>支付记录</text>
					<text>></text>
				</view>
			</view>
			<view class="item">
				<image src='../../static/ICON/icon_msg.png'></image>
				<view class="right">
					<text @click='goTousu'>举报投诉</text>
					<text>></text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				info: {}
			};
		},
		mounted() {
			uni.getStorage({
				key: 'userInfo',
				success: (res) => {
					this.info = res.data
					// console.log(res)
				}
			})	
		},
		methods:{
			goTousu(){
				uni.navigateTo({
					url:'../Tousu/Tousu'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.pinfo {
		margin-left: 20rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		border-bottom: 1px solid #ddd;
		padding: 40rpx 20rpx 40rpx 0;
		.pname {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: flex-start;

			text:nth-child(1) {
				font-weight: bolder;
				font-size: 48rpx;
			}

			text:nth-child(2) {
				color:#c8c8c8;
				font-size: 32rpx;
			}
		}
		image{
			width: 120rpx;
			height: 120rpx;
			border-radius: 60rpx;
		}
	}
	.list{
		.item{
			margin-left: 20rpx;
			display: flex;
			align-items: center;
			height: 100rpx;
			image{
				width: 60rpx;
				height: 60rpx;
				margin-right: 20rpx;
			}
			.right{
				flex:1;
				height: 100rpx;
				line-height: 100rpx;
				font-size: 30rpx;
				border-bottom: 1px solid #ddd;
				text:nth-child(1){
					display: inline-block;
					width: 90%;
				}
			}
		}
	}
</style>
