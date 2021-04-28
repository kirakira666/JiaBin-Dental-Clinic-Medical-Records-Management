<template>
	<view class="u-flex user-box u-p-l-30 u-p-r-20 u-p-b-30">
		<view class="u-m-r-10">
			<u-avatar src="D://kk.jpg" size="140"></u-avatar>
		</view>
		<view class="u-flex-1">
			<view class="u-font-18 u-p-b-20">{{wechatName}}</view>
			<view class="u-font-14 u-tips-color">微信号：{{wechatID}}</view>
		</view>
		<view class="u-m-l-10 u-p-10">
			<u-icon name="scan" color="#969799" size="28"></u-icon>
		</view>
		<view class="u-m-l-10 u-p-10">
			<u-icon name="arrow-right" color="#969799" size="28" @click="toCenter"></u-icon>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				pic:'../../static/kk.jpg',
				show:true,
				wechatName: '刘医生',
				wechatID: '8888888hggjhg'
			};
		},
		methods: {
			toCenter() {
				console.log("去个人中心")
			}
		}
	}
</script>

<style scoped>
	
	.data {
		display: inline-block;
	}
</style>
