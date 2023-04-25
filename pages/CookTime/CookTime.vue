<template>
	<view>
		<view class="top">
			<view class="left">
				<image src='../../static/ICON/icon_cha.png'></image>
				<text>已有{{planArr.length}}个行程</text>
			</view>
			<view class="right">
				<image src="../../static/ICON/77.png"></image>
				<text>历史</text>
			</view>
		</view>
		<view class="list">
			<PlanCard v-for='(item,index) in planArr' :key='index' :info='item'/>
		</view>
	</view>
</template>

<script>
	import PlanCard from '../../components/PlanCard/PlanCard.vue'
	import goodsJson from '../../static/goods-json.js'
	export default {
		components:{
		PlanCard
		},
		data() {
			return {
				planArr:[]
			};
		},
		methods:{
		},
			
		mounted(){
			/* uni.showModal({
				title: '提示',
				content: '这是一个模态弹窗',
				// showCancel:false, //不显示取消按钮
				confirmText:"确定",
				cancelText:"取消",
				success: function (res) {
					if (res.confirm) {
						console.log('用户点击确定');
						// 拨打电话
						uni.makePhoneCall({
							phoneNumber:'15527069211'
						})
					} else if (res.cancel) {
						console.log('用户点击取消');
					}
				}
			});
 */

			const userinfo = uni.getStorageSync('userInfo')
			// 判断用户是否登录
			/* if(userinfo){
				uni.showLoading({
					title: '加载中'
				});
				setTimeout(() => {
					this.planArr = goodsJson.planlist
					uni.hideLoading();
				}, 2000)
			} */
			this.planArr = goodsJson.planlist
		}
	}
</script>

<style lang="less" scoped>
	.list {
		width: 92%;
		margin: 0 auto;
		margin-top: 30rpx;
	
	}
	.top {
		width: 92%;
		margin: 0 auto;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding-top: 20rpx;
	
		.left {
			display: flex;
			align-items: center;
	
			image {
				width: 32rpx;
				height: 32rpx;
				margin-right: 10rpx;
			}
		}
	
		.right {
			display: flex;
			color: #ccc;
			align-items: center;
	
			image {
				width: 32rpx;
				height: 32rpx;
				margin-right: 10rpx;
			}
		}
	}
	
</style>
