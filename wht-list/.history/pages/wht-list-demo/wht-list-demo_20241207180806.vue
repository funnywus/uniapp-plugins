<template>
	<view class="container">
		<view class="example-title">基础列表</view>
		<wht-list-item title="标题文字" />

		
		<wht-list>
			<wht-list-item title="标题文字" />
			<wht-list-item title="标题文字" note="描述信息" />
			<wht-list-item title="标题文字" note="描述信息" rightText="右侧文字" />
		</wht-list>

		<view class="example-title">卡片列表</view>
		<wht-list card>
			<wht-list-item title="卡片列表" note="带阴影的列表项" showArrow />
			<wht-list-item title="链接跳转" link="navigateTo" to="/pages/index/index" />
		</wht-list>

		<view class="example-title">图文列表</view>
		<wht-list card>
			<wht-list-item 
				title="uni-app" 
				note="uni-app 是一个使用 Vue.js 开发所有前端应用的框架" 
				thumb="/static/logo.png"
				showArrow
			/>
			<wht-list-item 
				title="快速开发" 
				note="开发一次，多端覆盖，开发成本大幅度降低" 
				showExtraIcon 
				:extraIcon="{ type: 'fire-filled', color: '#ff6a3c' }"
			/>
		</wht-list>

		<view class="example-title">交互列表</view>
		<wht-list card>
			<wht-list-item 
				title="消息提醒" 
				showBadge 
				badgeText="12"
				showArrow
			/>
			<wht-list-item 
				title="系统通知" 
				showBadge 
				badgeText="新"
				badgeType="error"
				showArrow
			/>
			<wht-list-item 
				title="消息免打扰" 
				showSwitch 
				@switchChange="onSwitchChange"
			/>
		</wht-list>

		<view class="example-title">禁用状态</view>
		<wht-list card>
			<wht-list-item 
				title="禁用状态" 
				note="不可点击，不可切换"
				disabled 
				showSwitch
			/>
			<wht-list-item 
				title="禁用跳转" 
				note="不可点击跳转"
				disabled
				link="navigateTo" 
				to="/pages/index/index"
			/>
		</wht-list>

		<view class="example-title">自定义样式</view>
		<wht-list card>
			<wht-list-item>
				<template v-slot:header>
					<view class="custom-icon">
						<uni-icons type="star-filled" size="22" color="#ffc107"></uni-icons>
					</view>
				</template>
				<view class="custom-box">
					<text class="custom-title">自定义标题</text>
					<text class="custom-note">自定义描述文字</text>
				</view>
				<template v-slot:right>
					<uni-icons type="more-filled" size="20" color="#bbb"></uni-icons>
				</template>
			</wht-list-item>
		</wht-list>
	</view>
</template>

<script>

import whtListItem from '../../components/wht-list-item/wht-list-item.vue'
export default {
	
	data() {
		return {}
	},
	methods: {
		onSwitchChange(e) {
			uni.showToast({
				title: '开关状态：' + e.value,
				icon: 'none'
			})
		}
	}
}
</script>

<style lang="scss">
	page {
		background-color: #f5f7fa;
	}

	.container {
		padding: 10px;
	}

	.example-title {
		margin: 20px 10px 10px;
		font-size: 14px;
		color: #909399;
	}

	.custom-icon {
		margin-right: 12px;
	}

	.custom-box {
		display: flex;
		flex-direction: column;
		.custom-title {
			font-size: 14px;
			color: #303133;
		}
		.custom-note {
			margin-top: 6rpx;
			font-size: 12px;
			color: #909399;
		}
	}
</style>
