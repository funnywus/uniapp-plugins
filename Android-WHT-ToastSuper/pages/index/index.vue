<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
			<button @click="showToast('top')">显示顶部 Toast</button>
			<button @click="showToast('center')">显示中间 Toast</button>
			<button @click="showToast('bottom')">显示底部 Toast</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		methods: {
			showToast(position) {
				uni.requireNativePlugin('ToastPlugin').showToast('Hello, World!', 1, position);
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
		flex-direction: column;
		align-items: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}

	button {
		margin-top: 20rpx;
		padding: 10rpx 20rpx;
		background-color: #007aff;
		color: white;
		border: none;
		border-radius: 5rpx;
	}
</style>
