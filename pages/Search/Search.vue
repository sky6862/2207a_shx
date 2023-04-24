<template>
	<view>
		<view class="">
			搜索
		</view>
		<input type="text" placeholder="输入关键词" @blur="doSearch">
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			doSearch(){
				console.log(666)
			}
		}
	}
</script>

<style lang="less">

</style>
