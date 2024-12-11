<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<button class="demo-btn" @click="goToDemo">查看组件示例</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'wht-list 组件示例'
			}
		},
		onLoad() {

		},
		methods: {
			goToDemo() {
				uni.navigateTo({
					url: '/pages/wht-list-demo/wht-list-demo'
				})
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
		margin-bottom: 50rpx;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}

	.demo-btn {
		background-color: #007AFF;
		color: #fff;
		border-radius: 8rpx;
		padding: 20rpx 40rpx;
		font-size: 32rpx;
	}
</style>
