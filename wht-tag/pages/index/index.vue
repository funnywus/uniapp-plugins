<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<button class="demo-btn" @click="goToDemo">查看 wht-tag 组件示例</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'wht-tag 组件'
			}
		},
		onLoad() {

		},
		methods: {
			goToDemo() {
				uni.navigateTo({
					url: '/pages/wht-tag-demo/wht-tag-demo'
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
		background-color: #2979ff;
		color: #fff;
		font-size: 32rpx;
		padding: 20rpx 40rpx;
		border-radius: 8rpx;
	}

	.demo-btn:active {
		opacity: 0.8;
	}
</style>
