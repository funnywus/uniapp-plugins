<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{ title }}</text>
		</view>
		<button class="demo-btn" @click="goToDemo">查看wht-link演示</button>
	</view>
</template>

<script setup>
import { ref } from 'vue'

const title = ref('wht-link 超链接组件')

const goToDemo = () => {
	uni.navigateTo({
		url: '/pages/wht-link-demo/wht-link-demo'
	})
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
		margin-top: 30rpx;
		background-color: #409eff;
		color: #ffffff;
		border: none;
		border-radius: 8rpx;
		padding: 20rpx 40rpx;
	}
</style>
