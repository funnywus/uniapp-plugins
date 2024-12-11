<template>
	<view class="wht-list" :class="{'wht-list--border': border, 'wht-list--card': card}">
		<scroll-view 
			class="wht-list-scroll"
			scroll-y
			:refresher-enabled="true"
			:refresher-triggered="refresherTriggered"
			@refresherrefresh="onRefresh"
			@scrolltolower="onLoadMore"
		>
			<!-- 列表内容 -->
			<view class="wht-list-content">
				<slot></slot>
			</view>
			
			<!-- 加载状态 -->
			<view class="wht-list-status">
				<view v-if="loading" class="status-loading">
					<view class="loading-icon"></view>
					<text class="loading-text">加载中...</text>
				</view>
				<view v-else-if="error" class="status-error" @click="onErrorClick">
					<text class="error-text">{{ errorText }}</text>
				</view>
				<view v-else-if="finished" class="status-finished">
					<text class="finished-text">{{ finishedText }}</text>
				</view>
				<view v-else-if="list.length === 0" class="status-empty">
					<text class="empty-text">{{ emptyText }}</text>
				</view>
			</view>
		</scroll-view>
	</view>
</template>
<script>
/**
 * wht-list 列表组件
 * @description 一个支持下拉刷新和上拉加载的列表组件
 * @property {Array} list 列表数据
 * @property {Boolean} loading 是否处于加载状态
 * @property {Boolean} finished 是否已加载完所有数据
 * @property {Boolean} error 是否加载失败
 * @property {String} empty-text 空数据提示文字
 * @property {String} error-text 加载失败提示文字
 * @property {String} finished-text 加载完成提示文字
 * @property {Boolean} border 是否显示边框
 * @property {Boolean} card 是否使用卡片样式
 * @event {Function} loadmore 滚动到底部时触发
 * @event {Function} refresh 下拉刷新时触发
 * @event {Function} error-click 点击错误提示时触发
 */
export default {
	name: 'wht-list',
	props: {
		border: {
			type: Boolean,
			default: false
		},
		card: {
			type: Boolean,
			default: false
		},
		list: {
			type: Array,
			default() {
				return []
			}
		},
		loading: {
			type: Boolean,
			default: false
		},
		finished: {
			type: Boolean,
			default: false
		},
		error: {
			type: Boolean,
			default: false
		},
		emptyText: {
			type: String,
			default: '暂无数据'
		},
		errorText: {
			type: String,
			default: '加载失败，点击重试'
		},
		finishedText: {
			type: String,
			default: '没有更多数据了'
		}
	},
	data() {
		return {
			refresherTriggered: false
		}
	},
	methods: {
		// 触发加载更多
		onLoadMore() {
			if (!this.loading && !this.finished && !this.error) {
				this.$emit('loadmore')
			}
		},
		// 触发下拉刷新
		async onRefresh() {
			this.refresherTriggered = true
			this.$emit('refresh')
			// 等待父组件处理完刷新事件
			await this.$nextTick()
			setTimeout(() => {
				this.refresherTriggered = false
			}, 500)
		},
		// 点击错误提示
		onErrorClick() {
			this.$emit('error-click')
		}
	}
}
</script>
<style lang="scss" scoped>

.wht-list {
	display: block;
	width: 100%;
	background-color: $wht-list-bg-color;
	
	&--card {
		margin: $wht-list-card-margin;
		border-radius: $wht-list-card-radius;
		overflow: hidden;
		box-shadow: 0 1px 4px rgba(0, 0, 0, 0.08);
	}
}

.wht-list-scroll {
	height: 100%;
}

.wht-list-content {
	padding: 20rpx;
}

.wht-list-status {
	padding: 30rpx;
	display: flex;
	justify-content: center;
	align-items: center;
}

/* 加载状态样式 */
.status-loading {
	display: flex;
	align-items: center;
}

.loading-icon {
	width: 40rpx;
	height: 40rpx;
	margin-right: 10rpx;
	border: 4rpx solid #e5e5e5;
	border-top-color: #666;
	border-radius: 50%;
	animation: loading 0.8s linear infinite;
}

.loading-text {
	font-size: 28rpx;
	color: #999;
}

/* 错误状态样式 */
.status-error {
	padding: 20rpx;
}

.error-text {
	font-size: 28rpx;
	color: #999;
}

/* 完成状态样式 */
.status-finished {
	padding: 20rpx;
}

.finished-text {
	font-size: 28rpx;
	color: #999;
}

/* 空状态样式 */
.status-empty {
	padding: 40rpx;
}

.empty-text {
	font-size: 28rpx;
	color: #999;
}

@keyframes loading {
	0% {
		transform: rotate(0deg);
	}
	100% {
		transform: rotate(360deg);
	}
}
</style>
