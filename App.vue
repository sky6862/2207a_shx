<script>
	export default {
		onLaunch: function() {
			//表示整个应用加载 
			//如果已经登录过了(userInfo存放了数据) 不用再去登录页
			console.log(666)
			const info = uni.getStorageSync('userInfo');	
			
			/* if(!info){
				uni.navigateTo({
					url:'pages/Profile/Profile'
				})
			} */
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
			// uni.requestPayment({
			//     provider: 'wxpay',
			//     timeStamp: String(Date.now()),
			//     nonceStr: 'A1B2C3D4E5',
			//     package: 'prepay_id=wx20180101abcdefg',
			//     signType: 'MD5',
			//     paySign: '',
			//     success: function (res) {
			//         console.log('success:' + JSON.stringify(res));
			//     },
			//     fail: function (err) {
			//         console.log('fail:' + JSON.stringify(err));
			//     }
			// });
		}
	}
</script>

<style>
	/*每个页面公共css */
	page{
		width: 100%;
		height: 100%;
	}
	view{
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
	
</style>
