<template>
	<view class="content">
		<!-- 顶部导航 -->
		<view class="nav">
			<text>吸顶组件演示</text>
		</view>
		
		<!-- 基础用法演示区域 -->
		<view class="demo-section">
			<view class="section-title">基础用法</view>
			<view class="placeholder">向下滚动查看效果</view>
			<wht-sticky>
				<view class="sticky-demo">
					<text>基础吸顶效果</text>
				</view>
			</wht-sticky>
			<view class="placeholder">继续向下滚动</view>
		</view>
		
		<!-- 自定义距离演示区域 -->
		<view class="demo-section">
			<view class="section-title">自定义距离</view>
			<wht-sticky :offset-top="50">
				<view class="sticky-demo sticky-demo2">
					<text>距顶部50px吸顶</text>
				</view>
			</wht-sticky>
			<view class="placeholder">继续向下滚动</view>
		</view>
		
		<!-- 自定义样式演示区域 -->
		<view class="demo-section">
			<view class="section-title">自定义样式</view>
			<wht-sticky :z-index="999">
				<view class="sticky-demo sticky-demo3">
					<view class="custom-header">
						<text>自定义样式吸顶效果</text>
					</view>
				</view>
			</wht-sticky>
			<view class="placeholder">继续向下滚动</view>
		</view>
	</view>
</template>

<script>

export default {
	data() {
		return {
			title: 'Sticky Demo'
		}
	}
}
</script>

<style>
	.content {
		padding: 15px;
	}
	.placeholder {
		height: 500px;
		background: linear-gradient(to bottom, #f5f5f5, #e5e5e5);
		margin: 20px 0;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #999;
		font-size: 14px;
	}
	.sticky-demo {
		padding: 20px;
		text-align: center;
		background: #007AFF;
		color: #fff;
	}
	.sticky-demo2 {
		background: #4CD964;
	}
	.sticky-demo3 {
		background: #FFC0CB;
	}
	.custom-header {
		padding: 10px;
		background: #fff;
		border-bottom: 1px solid #ddd;
	}
	.nav {
		height: 50px;
		background: #007AFF;
		color: #fff;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 18px;
		font-weight: bold;
	}
	.demo-section {
		margin-bottom: 50px;
	}
	.section-title {
		padding: 20px 15px;
		font-size: 16px;
		color: #666;
		background: #f8f8f8;
		margin-bottom: 20px;
	}
</style>
