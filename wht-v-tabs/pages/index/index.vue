<template>
	<view class="container">
		<wht-v-tabs 
			:tabList="categoryList" 
			@change="onTabChange"
			class="category-tabs"
		>
			<template v-for="(category, index) in categoryList" :key="index" #[`content_${index}`]>
				<view class="goods-list">
					<view class="goods-grid">
						<view 
							class="goods-item"
							v-for="(item, idx) in category.goods" 
							:key="idx"
							@click="onGoodsClick(item)"
						>
							<image class="goods-img" :src="item.image" mode="aspectFill"></image>
							<view class="goods-info">
								<text class="goods-name">{{item.name}}</text>
								<text class="goods-desc">{{item.desc}}</text>
								<view class="goods-price-wrap">
									<text class="price-symbol">¥</text>
									<text class="price-num">{{item.price}}</text>
								</view>
							</view>
						</view>
					</view>
				</view>
			</template>
		</wht-v-tabs>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				categoryList: [
					{
						id: 1,
						name: '热销商品',
						icon: '/static/category/hot.png',
						banner: '/static/banner/1.jpg',
						desc: '人气爆款',
						goods: [
							{
								id: 101,
								name: '商品名称商品名称商品名称',
								desc: '商品描述信息',
								price: '99.00',
								image: 'https://via.placeholder.com/200'
							},
							{
								id: 102,
								name: '商品名称商品名称',
								desc: '商品描述信息',
								price: '199.00',
								image: 'https://via.placeholder.com/200'
							},
							{
								id: 103,
								name: '商品名称商品名称',
								desc: '商品描述信息',
								price: '299.00',
								image: 'https://via.placeholder.com/200'
							}
						]
					},
					{
						id: 2,
						name: '新品上市',
						icon: '/static/category/new.png',
						banner: '/static/banner/2.jpg',
						desc: '新品推荐',
						goods: [
							{
								id: 201,
								name: '新品商品名称',
								desc: '商品描述信息',
								price: '88.00',
								image: 'https://via.placeholder.com/200'
							},
							{
								id: 202,
								name: '新品商品名称',
								desc: '商品描述信息',
								price: '188.00',
								image: 'https://via.placeholder.com/200'
							}
						]
					},
					{
						id: 3,
						name: '居家生活',
						icon: '/static/category/home.png',
						banner: '/static/banner/3.jpg',
						desc: '居家好物',
						goods: Array(6).fill().map((_, idx) => ({
							id: 300 + idx,
							name: '居家商品' + (idx + 1),
							desc: '商品描述信息',
							price: ((idx + 1) * 100).toFixed(2),
							image: 'https://via.placeholder.com/200'
						}))
					},
					{
						id: 4,
						name: '服饰鞋包',
						icon: '/static/category/clothes.png',
						banner: '/static/banner/4.jpg',
						desc: '潮流精选',
						goods: Array(8).fill().map((_, idx) => ({
							id: 400 + idx,
							name: '时尚商品' + (idx + 1),
							desc: '商品描述信息',
							price: ((idx + 1) * 150).toFixed(2),
							image: 'https://via.placeholder.com/200'
						}))
					},
					{
						id: 5,
						name: '美妆护肤',
						icon: '/static/category/beauty.png',
						banner: '/static/banner/5.jpg',
						desc: '美妆个护',
						goods: Array(6).fill().map((_, idx) => ({
							id: 500 + idx,
							name: '美妆商品' + (idx + 1),
							desc: '商品描述信息',
							price: ((idx + 1) * 120).toFixed(2),
							image: 'https://via.placeholder.com/200'
						}))
					}
				]
			}
		},
		methods: {
			onTabChange(index) {
				console.log('切换分类:', this.categoryList[index].name)
			},
			onGoodsClick(goods) {
				console.log('点击商品:', goods)
				// 跳转到商品详情页
				uni.navigateTo({
					url: `/pages/goods/detail?id=${goods.id}`
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		height: 100vh;
		background: #f8f8f8;
	}

	.category-tabs {
		height: 100%;
	}

	.goods-list {
		padding: 20rpx;
	}

	.goods-grid {
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		gap: 20rpx;
	}

	.goods-item {
		background: #fff;
		border-radius: 12rpx;
		overflow: hidden;
		
		.goods-img {
			width: 100%;
			height: 260rpx;
		}
		
		.goods-info {
			padding: 16rpx;
			
			.goods-name {
				font-size: 26rpx;
				color: #333;
				line-height: 1.4;
				height: 72rpx;
				display: -webkit-box;
				-webkit-box-orient: vertical;
				-webkit-line-clamp: 2;
				overflow: hidden;
			}
			
			.goods-desc {
				font-size: 24rpx;
				color: #999;
				margin: 8rpx 0;
				white-space: nowrap;
				overflow: hidden;
				text-overflow: ellipsis;
			}
			
			.goods-price-wrap {
				margin-top: 12rpx;
				
				.price-symbol {
					font-size: 24rpx;
					color: #ff4d4f;
				}
				
				.price-num {
					font-size: 32rpx;
					font-weight: bold;
					color: #ff4d4f;
				}
			}
		}
	}

	// 骨架屏动画
	@keyframes skeleton {
		0% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0 50%;
		}
	}

	.skeleton {
		background: linear-gradient(90deg, #f2f2f2 25%, #e6e6e6 37%, #f2f2f2 63%);
		background-size: 400% 100%;
		animation: skeleton 1.4s ease infinite;
	}
</style>
