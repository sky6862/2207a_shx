<template>
	<view>
		<view class="top">
			<view>投诉类型</view>
			<view>
				<text @click="changeType(1)" :class="msg_type == 1 ? 'active':''">服务态度</text>
				<text @click="changeType(2)" :class="msg_type == 2 ? 'active':''">菜品问题</text>
				<text @click="changeType(3)" :class="msg_type == 3 ? 'active':''">付款问题</text>
			</view>
		</view>
		<view class='main'>
			<textarea :placeholder="tips" v-model="msg"></textarea>
		</view>
		<view class="img">
			<!-- 上传成功后，显示图片 -->
			<!-- <image :src="v" v-for="(v,k) in imgArr" :key="'img_'+k"></image> -->
			<view class="pre_img">
				<view class="" v-for="(v,k) in imgArr" :key="'img_'+k" class="item">
					<text @click="delImg(v,k)">Clost</text>
					<image :src="v"></image> 
				</view>
			</view>
			
			<view class='btn' @click="upLoadImg">
				＋
			</view>
		</view>
		
		<view class="sbt" @click="saveTouSu">
			提交
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			    msg_type:1,
				msg:"",
				imgArr:[], //上传成功后，得到的文件地址数组
				tips:"输入投诉详细说明(选填)"
			};
		},
		methods: {
			changeType(num){
				this.msg_type = num;
				if(num == 1){
					this.tips = "服务态度:"
				}
				else if(num == 2){
					this.tips = "菜品问题:"
				}
				else{
					this.tips = "付款问题:"
				}
			},
			//上传图片：一次传一个
			upLoadImg() {
				
				// A:选择图片 uni.chooseImage  https://zh.uniapp.dcloud.io/api/media/image.html
				//1.调用相关API传图片
				// B:上传图片  
				//2.将这个图片上传到服务器
				//3.服务器应该返回这个图片的服务器地址
				//4.将返回的线上地址图片渲染到页面
				uni.chooseImage({
					count: 6, //默认9
					// sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					extension:['.jpg','.gif','.png'],
					sourceType: ['album'], //从相册选择
					success: (res)=> {
						console.log(res);
						uni.uploadFile({
							url:"http://api.brqc.com.cn/cpz/shxmp/upload",
							name:"pic",
							filePath:res.tempFilePaths[0],//文件路径
							success:(res)=> {
								// res 返回一个字符串的结果，需要把json格式的字符中转为json对象
						        let res_data = JSON.parse(res.data)
								console.log(res,res_data)
								/* 
								res_data = 
								{
									code: 0
									data: {pic: 'http://api.brqc.com.cn/cpz/uploads/ffb6db7b09a1fdc297b39f97dd7bbbab.GIF', originalname: '4.GIF', extname: '.GIF', size: '0.09 MB'}
									msg: "图片上传成功"
									
								}
								 */
								let pic_url = res_data.data.pic;
								this.imgArr.push(pic_url)
							}
						})
					}
				});
			},
			// 删除文件
			delImg(pic_url,index){
				// 1.页面删除-imgArr元素删除
				this.imgArr.splice(index,1)
				// 2.发请求，告诉后端，要删除这个已经上传过的图片
				// uni.request({
				// 	url:
				// })
			},
			//提交表单
			saveTouSu(){
				// 1.获取要提交的数据(类型、说明，图片(图片地址))
				// 2.发请求，保存投诉内容
				console.log(this.msg_type,this.msg,JSON.stringify(this.imgArr))
				
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

			text.active{
				background-color: #de8116;
				color: #fff;
			}
		}
	}

	.main {
		padding: 40rpx;
		height: 30vh;
	}
    .sbt{
		padding: 15rpx;
		background-color: rebeccapurple;
		text-align: center;
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
		
		.pre_img {
			.item{
				position: relative;
				text{
					position: absolute;
					left:0;
					top:0;
					z-index: 100;
				}
			}
		}
	}
</style>
