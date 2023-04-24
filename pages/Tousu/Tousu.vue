<template>
	<view>
		<view class="top">
			<view>投诉类型</view>
			<view>
				<text>服务态度</text>
				<text>菜品问题</text>
				<text>付款问题</text>
			</view>
		</view>
		<view class='main'>
			<textarea placeholder="输入投诉详细说明(选填)"></textarea>
		</view>
		<view class="img">
			<view class='btn' @click="upLoadImg">
				＋
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imgArr:[],
				baseUrl:'https://slimmings.healthmach.com'
			};
		},
		methods: {
			upLoadImg() {
				//1.调用相关API传图片
				//2.将这个图片上传到服务器
				//3.服务器应该返回这个图片的服务器地址
				//4.将返回的线上地址图片渲染到页面
				uni.chooseImage({
					count: 6, //默认9
					// sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					// sourceType: ['album'], //从相册选择
					success: (res)=> {
						uni.uploadFile({
							url: 'https://slimmings.healthmach.com/api/plugs/uploads', 
							filePath: res.tempFilePaths[0],
							name: 'files',
							success: (uploadFileRes) => {
								let data = JSON.parse(uploadFileRes.data);
								this.imgArr.push(this.baseUrl+data.data)
								console.log(this.imgArr)
							}
						});
					}
				});
			}
		}
	}
</script>

<style lang="less" scoped>
	.top {
		padding: 40rpx;
		border-bottom: 1px solid #ddd;

		view:nth-child(1) {
			font-weight: bolder;
		}

		view:nth-child(2) {
			margin-top: 30rpx;

			text {
				margin-right: 12rpx;
				border-radius: 40rpx;
				padding: 12rpx 20rpx;
				border: 1px solid #ddd;
			}

			text:nth-child(1) {
				background-color: #de8116;
				color: #fff;
			}
		}
	}

	.main {
		padding: 40rpx;
		height: 30vh;
	}

	.img {
		padding: 40rpx;

		.btn {
			width: 200rpx;
			height: 200rpx;
			background-color: #ddd;
			line-height: 200rpx;
			font-size: 120rpx;
			color: #959595;
			text-align: center;
		}
	}
</style>
