<template>
	<view>
		<view class="">
		 周边	
		</view>
		<button @click="pay">立即购买</button>
		
		<open-data type="userNickName"></open-data>
		<open-data type="userAvatarUrl"></open-data>
		
		<button open-type="getUserInfo" @getuserinfo="userInfo">获取</button>
		
		<button @click="getInfo">获取个人信息</button>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			// 登录，支付 需要在 开发者工具中测试
			pay(){
				// 1.调用 登录接口-获取登录凭证
				uni.login({
					timeout:3000,
					success(res) {
						// 登录成功，获取登录凭证
						console.log(res)
						
						// 2.保存 凭证
						uni.setStorageSync("login_code",res.code)
						
						// 3.根据登录获取到的code，请求自己的服务器（公司自己后端写），获取openid
						/* 
						   uni.request({
						     url:"https://aaa.com/getOpenId?code=0e3frkGa1gJybF0VxxHa
						     success(res){
						         // 获取openid
						     }
						   })
						 */
						
						/* 
						// 4.创建支付订单
						  uni.request({url:"https://aaa.com/createPayOrder"}) 
						*/
					   
					   // 5.调用支付方法,进行支付
					   /* 
					   uni.requestPayment({
							 provider: 'wxpay', //支付方式
							timeStamp: String(Date.now()),
							nonceStr: 'A1B2C3D4E5', //随机字符串
							package: 'prepay_id=wx20180101abcdefg', //预支付订单好
							signType: 'MD5',//签名算法
							paySign: 'jowhgioewgo9y0wfw90', //签名
							success: function (res) {
								console.log('success:' + JSON.stringify(res));
							},
							fail: function (err) {
								console.log('fail:' + JSON.stringify(err));
							}
					   });
					   */
						
					}
				})
			},
			userInfo(res){
				console.log(res)
			},
			getInfo(){
				if(uni.getUserProfile){
					uni.getUserProfile({
						desc:"请授权登录,更好的使用本小程序",
						success(res) {
							console.log(res,res.userInfo)
						}
					})
				}
				// 
			}
		}
	}
</script>

<style lang="less">

</style>
