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
			const userinfo = uni.getStorageSync('userInfo')
			if(userinfo){
				uni.showLoading({
					title: '加载中'
				});
				setTimeout(() => {
					this.planArr = goodsJson.planlist
					uni.hideLoading();
				}, 2000)
			}
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
