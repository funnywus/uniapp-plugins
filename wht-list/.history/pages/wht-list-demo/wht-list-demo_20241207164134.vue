<![CDATA[<template>
	<view class="container">
		<view class="section">
			<view class="section-title">基础用法</view>
			<wht-list :list="basicList" @loadmore="onLoadMore" @refresh="onRefresh">
				<template #default="{ item }">
					<view class="list-item">
						<text class="item-title">{{item.title}}</text>
						<text class="item-desc">{{item.description}}</text>
					</view>
				</template>
			</wht-list>
		</view>
		
		<view class="section">
			<view class="section-title">高级用法</view>
			<wht-list 
				:list="advancedList" 
				:loading="loading"
				:finished="finished"
				:error="error"
				empty-text="暂无数据"
				error-text="加载失败，点击重试"
				@loadmore="onAdvancedLoadMore" 
				@refresh="onAdvancedRefresh"
				@error-click="onErrorClick"
			>
				<template #default="{ item }">
					<view class="advanced-item">
						<image class="item-image" :src="item.image" mode="aspectFill"></image>
						<view class="item-content">
							<text class="item-title">{{item.title}}</text>
							<text class="item-desc">{{item.description}}</text>
							<text class="item-time">{{item.time}}</text>
						</view>
					</view>
				</template>
			</wht-list>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				basicList: [],
				advancedList: [],
				loading: false,
				finished: false,
				error: false,
				page: 1,
				advancedPage: 1
			}
		},
		onLoad() {
			this.loadBasicData()
			this.loadAdvancedData()
		},
		methods: {
			// 基础用法相关方法
			loadBasicData() {
				// 模拟数据加载
				setTimeout(() => {
					const newData = Array.from({length: 10}, (_, index) => ({
						id: this.basicList.length + index + 1,
						title: `标题 ${this.basicList.length + index + 1}`,
						description: '这是一段描述文字，用于演示基础列表的展示效果'
					}))
					this.basicList = [...this.basicList, ...newData]
				}, 1000)
			},
			onLoadMore() {
				this.loadBasicData()
			},
			onRefresh() {
				this.basicList = []
				this.loadBasicData()
			},
			
			// 高级用法相关方法
			async loadAdvancedData() {
				if (this.loading || this.finished) return
				this.loading = true
				this.error = false
				
				try {
					// 模拟异步数据加载
					await new Promise(resolve => setTimeout(resolve, 1500))
					
					// 模拟数据
					const newData = Array.from({length: 5}, (_, index) => ({
						id: this.advancedList.length + index + 1,
						title: `高级列表标题 ${this.advancedList.length + index + 1}`,
						description: '这是一段较长的描述文字，用于演示高级列表的展示效果，包含更多的信息和交互',
						image: 'https://via.placeholder.com/100',
						time: new Date().toLocaleString()
					}))
					
					this.advancedList = [...this.advancedList, ...newData]
					this.advancedPage++
					
					// 模拟数据加载完成
					if (this.advancedPage > 4) {
						this.finished = true
					}
				} catch (e) {
					this.error = true
				} finally {
					this.loading = false
				}
			},
			onAdvancedLoadMore() {
				this.loadAdvancedData()
			},
			onAdvancedRefresh() {
				this.advancedList = []
				this.advancedPage = 1
				this.finished = false
				this.loadAdvancedData()
			},
			onErrorClick() {
				this.loadAdvancedData()
			}
		}
	}
</script>

<style>
	.container {
		padding: 20rpx;
	}
	
	.section {
		margin-bottom: 40rpx;
	}
	
	.section-title {
		font-size: 32rpx;
		font-weight: bold;
		margin-bottom: 20rpx;
		padding: 0 20rpx;
	}
	
	/* 基础列表样式 */
	.list-item {
		padding: 20rpx;
		background-color: #ffffff;
		margin-bottom: 20rpx;
		border-radius: 12rpx;
	}
	
	.list-item .item-title {
		font-size: 28rpx;
		color: #333333;
		margin-bottom: 10rpx;
		display: block;
	}
	
	.list-item .item-desc {
		font-size: 24rpx;
		color: #999999;
		display: block;
	}
	
	/* 高级列表样式 */
	.advanced-item {
		display: flex;
		padding: 20rpx;
		background-color: #ffffff;
		margin-bottom: 20rpx;
		border-radius: 12rpx;
	}
	
	.advanced-item .item-image {
		width: 160rpx;
		height: 160rpx;
		border-radius: 8rpx;
		margin-right: 20rpx;
	}
	
	.advanced-item .item-content {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}
	
	.advanced-item .item-title {
		font-size: 28rpx;
		color: #333333;
		margin-bottom: 10rpx;
	}
	
	.advanced-item .item-desc {
		font-size: 24rpx;
		color: #666666;
		margin-bottom: 10rpx;
	}
	
	.advanced-item .item-time {
		font-size: 22rpx;
		color: #999999;
	}
</style>]]>
