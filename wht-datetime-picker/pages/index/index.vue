<template>
	<view class="content">
		<button class="nav-btn" @click="goToDemo">日期时间选择器演示</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {
			goToDemo() {
				uni.navigateTo({
					url: '/pages/wht-datetime-picker-demo/wht-datetime-picker-demo'
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
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}

	.nav-btn {
		margin: 20rpx;
		background-color: #007aff;
		color: #fff;
	}
</style>
