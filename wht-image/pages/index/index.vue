<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<button class="demo-btn" @click="goToDemo">查看图片组件示例</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'wht-image 图片组件'
			}
		},
		onLoad() {

		},
		methods: {
			goToDemo() {
				uni.navigateTo({
					url: '/pages/wht-image-demo/wht-image-demo'
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
		margin-bottom: 60rpx;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}

	.demo-btn {
		background-color: #1989fa;
		color: #fff;
		border-radius: 80rpx;
		padding: 20rpx 60rpx;
		font-size: 32rpx;
		border: none;
	}

	.demo-btn:active {
		opacity: 0.8;
	}
</style>
