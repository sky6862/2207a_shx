<template>
	<view class='bgc'>
		<!-- 登录前的背景图状态 -->
		<image src='../../static/ICON/w4.jpg' mode="aspectFill"></image>
		<button type="primary" open-type="getUserInfo" @click='getUser'>点我授权</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},
		methods: {
			getUser() {
				// console.log(detail)
				// //将detail.detail.rawData这里的数据保存起来
				// uni.setStorage({
				//     key: 'userInfo',
				//     data: detail.detail.rawData,
				//     success: function () {
				//        uni.switchTab({
				//            url: '../Loaded/Loaded'
				//        });
				//     }
				// });
				uni.getUserProfile( //调用这个API实现信息的授权
					{
						desc: '是否授权登录四海香小程序', //必须写

						success: function(res) {
							uni.setStorage({
								key: 'userInfo',
								data: res.userInfo,
								success: function() {
									uni.switchTab({
										url: '../Loaded/Loaded'
									});
								}
							})
						},
						fail: function(err) {
							// console.log(err, 111)
						}
					})
			}
		}
	}
</script>

<style lang="less" scoped>
	.bgc {
		position: relative;
		height: 100%;

		image {
			width: 100%;
			height: 100%;
		}

		button {
			position: absolute;
			left: 50%;
			top: 50%;
			transform: translate(-50%, 250%);
			// height: 80rpx;
		}

		;
	}
</style>
