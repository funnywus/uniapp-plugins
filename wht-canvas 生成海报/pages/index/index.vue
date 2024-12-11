<template>
	<view class="content">
		<!-- 预览区域 -->
		<view class="preview-area" @click="showShareModal">
			<image 
				src="https://fastly.picsum.photos/id/49/2000/3000.jpg?hmac=_Ilec99N952SH847dPe_bctzaqrFvn9lWJyAuK0GtQU" 
				mode="aspectFit" 
				class="preview-image"
			></image>
			<view class="preview-tip">
				<text class="preview-text">点击生成海报</text>
			</view>
		</view>
		
		<!-- 分享弹窗 -->
		<view class="share-modal" v-if="showShare" @click="closeShare">
			<view class="share-content" @click.stop>
				<view class="share-header">
					<text class="share-title">分享海报</text>
					<text class="close-btn" @click="closeShare">×</text>
				</view>
				
				<view class="share-body">
					<!-- 海报画布 -->
					<wht-canvas-poster
						ref="poster"
						:width="300"
						:height="450"
						:poster-config="posterConfig"
						@canvasReady="onCanvasReady"
						@drawn="onDrawn"
						></wht-canvas-poster>
					
					<!-- 操作按钮 -->
					<button @click="savePoster" type="primary" class="action-btn">保存到相册</button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				showShare: false,
				posterConfig: {
					background: '#ffffff',
					elements: [
						{
							type: 'image',
							src: 'https://fastly.picsum.photos/id/49/2000/3000.jpg?hmac=_Ilec99N952SH847dPe_bctzaqrFvn9lWJyAuK0GtQU',
							x: 1,
							y: 2,
							maxWidth: 50,
							maxHeight: 50,
							margin: {
								top: 10,
								left: 10
							}
						}
					]
				}
			}
		},
		methods: {
			showShareModal() {
				this.showShare = true
				// 显示弹窗后自动生成海报
				this.$nextTick(() => {
					this.generatePoster()
				})
			},
			
			closeShare() {
				this.showShare = false
			},
			
			async generatePoster() {
				if (!this.$refs.poster.ctx) {
					uni.showToast({
						title: '画布未准备就绪',
						icon: 'none'
					})
					return
				}
				
				uni.showLoading({
					title: '生成中...'
				})
				
				try {
					await this.$refs.poster.draw()
					uni.hideLoading()
				} catch (error) {
					uni.hideLoading()
					uni.showToast({
						title: '生成失败',
						icon: 'none'
					})
				}
			},
			
			async savePoster() {
				if (!this.$refs.poster.ctx) {
					uni.showToast({
						title: '请先生成海报',
						icon: 'none'
					})
					return
				}
				await this.$refs.poster.saveToAlbum()
			},
			
			onCanvasReady() {
				console.log('画布准备就绪')
				this.generatePoster()
			},
			
			onDrawn() {
				console.log('海报绘制完成')
			}
		}
	}
</script>

<style>
	.content {
		padding: 40rpx;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		min-height: 100vh;
		background-color: #f8f8f8;
	}

	.preview-area {
		width: 100%;
		max-width: 600rpx;
		background: #ffffff;
		border-radius: 24rpx;
		box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
		overflow: hidden;
		position: relative;
		transition: transform 0.2s;
	}

	.preview-area:active {
		transform: scale(0.98);
	}

	.preview-image {
		width: 100%;
		height: 600rpx;
		display: block;
		object-fit: cover;
	}

	.preview-tip {
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		padding: 24rpx 0;
		background: linear-gradient(to top, rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0));
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.preview-text {
		color: #ffffff;
		font-size: 28rpx;
		font-weight: 500;
	}

	.share-modal {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: rgba(0, 0, 0, 0.7);
		z-index: 999;
		display: flex;
		align-items: center;
		justify-content: center;
		animation: fadeIn 0.2s ease-out;
	}

	.share-content {
		width: 90%;
		max-width: 600rpx;
		background-color: #ffffff;
		border-radius: 24rpx;
		overflow: hidden;
		animation: slideUp 0.3s ease-out;
	}

	.share-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 24rpx 32rpx;
		border-bottom: 1px solid #f0f0f0;
	}

	.share-title {
		font-size: 32rpx;
		font-weight: 600;
		color: #333333;
	}

	.close-btn {
		font-size: 48rpx;
		color: #999999;
		padding: 16rpx;
		margin: -16rpx;
		line-height: 1;
	}

	.share-body {
		padding: 32rpx;
	}

	.action-btn {
		margin-top: 32rpx;
		width: 100%;
		height: 88rpx;
		line-height: 88rpx;
		background: #07c160;
		color: #ffffff;
		font-size: 32rpx;
		font-weight: 500;
		border-radius: 44rpx;
		border: none;
	}

	.action-btn:active {
		opacity: 0.9;
		transform: scale(0.98);
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	@keyframes slideUp {
		from {
			transform: translateY(50rpx);
			opacity: 0;
		}
		to {
			transform: translateY(0);
			opacity: 1;
		}
	}
</style>
