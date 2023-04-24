<template>
	<view class="item">
		<image :src='info.img'></image>
		<text>{{info.name}}</text>
		<uni-rate :readonly="true" :value="2" :size="15"  class='starRate'/>
	</view>
</template>

<script>
	export default {
		props: ['info'],
		name: "CookerCard",
		data() {
			return {

			};
		}
	}
</script>

<style lang="less">
	.item {
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
		width: 220rpx;
		height: 280rpx;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

		image {
			width: 140rpx;
			height: 140rpx;
			border-radius: 50%;
		}
		.starRate{
			margin-top: 16rpx;
		}
	}
</style>
