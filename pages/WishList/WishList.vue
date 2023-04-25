<template>
	<view>
		<view class="show" v-if="isshow===true&&dataArr.length">
			<!-- 顶部收藏区域 -->
			<view class="top">
				<view class="left">
					<image src='../../static/ICON/icon_cha.png'></image>
					<text>已收藏{{dataArr.length}}个餐宴</text>
				</view>
				<view class="right">
					<image src="../../static/ICON/icon_clear.png"></image>
					<text @click='clearAll'>清空</text>
				</view>
			</view>
			<!-- 卡片展示区域 -->
			<view class="list">
				<FoodCard v-for="(item,index) in dataArr" :key='item.id' :info='item' @deleteOne='deleteOne'></FoodCard>
				<!-- 父亲在子组件身上绑定自定义事件 -->
			</view>
		</view>
		
		<view class="hide" v-if="isshow===true&&dataArr.length===0">
			<view class="top">
				<view class="left">
					<image src='../../static/ICON/icon_cha.png'></image>
					<text>已收藏{{dataArr.length}}个餐宴</text>
				</view>
				<view class="right">
					<image src="../../static/ICON/icon_clear.png"></image>
					<text @click='clearAll'>清空</text>
				</view>
			</view>
			<view class="noOrder">
				<image src="../../static/ICON/nomore2.png" mode="aspectFit"></image>
			</view>
		</view>
	</view>
</template>

<script>
	import FoodCard from '../../components/FoodCard/FoodCard.vue'
	import goodsJson from '../../static/goods-json.js'
	export default {
		components: {
			FoodCard
		},
		data() {
			return {
				dataArr: [],
				isshow: false
			};
		},
		mounted() {
			uni.showLoading({
				title: '加载中'
			});
			setTimeout(() => {
				this.dataArr = goodsJson.goodslist
				this.isshow = true
				uni.hideLoading();
			}, 2000)
		},
		methods: {
			clearAll() {
				//清空dataArr这个数组
				// console.log(this)
				this.dataArr.splice(0)
			},
			deleteOne(id) {
				//删除数组中点击的那一项
				// 1.es6一个数组方法 通过id找到具体的数组元素
				// let targetIndex = this.dataArr.findIndex((item)=>{
				// 	return item.id===id
				// })
				// this.dataArr.splice(targetIndex,1)
				//2.es5数组的过滤方法
				this.dataArr = this.dataArr.filter((item) => {
					return item.id !== id
				})
			}
		},

		onPullDownRefresh() {
			uni.showLoading({
				title: '刷新中'
			});
			//重新获取一下数据
			setTimeout(() => {
				// 这里要重新发送ajax请求
				uni.hideLoading();
				uni.stopPullDownRefresh(); //停止下拉动作
			}, 2000)
		},
		onReachBottom() {
			console.log(11)
			uni.showLoading({
				title: '加载更多数据中'
			});
			//加载下一屏数据
			setTimeout(() => {
				let newData = JSON.parse(JSON.stringify(goodsJson.goodslist))
				console.log(newData)
				newData.forEach((item)=>{
					item.id = String(Number(item.id)+this.dataArr.length)
				})
				this.dataArr=[...this.dataArr,...newData]//react是推荐这么做的 
				// this.dataArr.push(...newData)//vue推荐这么写 uniapp中不能这么写了
				uni.hideLoading();
			}, 2000)
		}
	}
</script>

<style lang="less">
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

			;
		}
	}

	.list {
		width: 92%;
		margin: 0 auto;
		margin-top: 30rpx;

	}

	.hide {
		.noOrder {
			text-align: center;

			image {
				width: 300rpx;
				margin-top: 200rpx;
			}

			;
		}
	}
</style>
