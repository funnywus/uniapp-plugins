<template>
	<view
		:class="{'wht-list-item--disabled': disabled}"
		:hover-class="(!clickable && !link) || disabled || showSwitch ? '' : 'wht-list-item--hover'"
		class="wht-list-item"
		@click="onClick"
	>
		<view class="wht-list-item__container">
			<view class="wht-list-item__header">
				<slot name="header">
					<view v-if="thumb" class="wht-list-item__icon">
						<image :src="thumb" class="wht-list-item__icon-img" />
					</view>
					<view v-else-if="showExtraIcon" class="wht-list-item__icon">
						<uni-icons :color="extraIcon.color" :size="extraIcon.size" :type="extraIcon.type" />
					</view>
				</slot>
			</view>

			<view class="wht-list-item__content">
				<slot>
					<text class="wht-list-item__content-title">{{ title }}</text>
					<text v-if="note" class="wht-list-item__content-note">{{ note }}</text>
				</slot>
			</view>

			<view class="wht-list-item__extra">
				<slot name="right">
					<text v-if="rightText" class="wht-list-item__extra-text">{{ rightText }}</text>
					<uni-badge v-if="showBadge" :type="badgeType" :text="badgeText" />
					<switch v-if="showSwitch" :disabled="disabled" :checked="switchChecked"
						@change="onSwitchChange" />
					<uni-icons v-if="showArrow || link" :size="16" class="wht-list-item__extra-icon-arrow"
						type="arrowright" />
				</slot>
			</view>
		</view>
	</view>
</template>

<script>
	/**
	 * ListItem 列表子组件
	 * @description 列表子组件
	 * @property {String} 	title 							标题
	 * @property {String} 	note 							描述
	 * @property {String} 	thumb 							左侧缩略图，若thumb有值，则不会显示扩展图标
	 * @property {String} 	rightText 						右侧文字内容
	 * @property {Boolean} 	disabled = [true|false] 			是否禁用
	 * @property {Boolean} 	clickable = [true|false] 		是否开启点击反馈
	 * @property {String} 	link = [navigateTo|redirectTo|reLaunch|switchTab] 是否展示右侧箭头并开启点击跳转
	 * @property {String | PageURIString} 	to  			跳转目标页面
	 * @property {Boolean} 	showBadge = [true|false] 		是否显示数字角标
	 * @property {String} 	badgeText 						数字角标内容
	 * @property {String} 	badgeType 						数字角标类型，参考[uni-badge](https://ext.dcloud.net.cn/plugin?id=21)
	 * @property {Object}   	extraIcon 						扩展图标参数，格式为 {color: '#4cd964',size: '22',type: 'spinner'}
	 * @property {Boolean} 	showSwitch = [true|false] 		是否显示Switch
	 * @property {Boolean} 	switchChecked = [true|false] 	Switch是否被选中
	 * @event {Function} 	click 							点击 uniListItem 触发事件
	 * @event {Function} 	switchChange 					点击切换 Switch 时触发
	 */
	export default {
		name: 'wht-list-item',
		props: {
			title: {
				type: String,
				default: ''
			},
			note: {
				type: String,
				default: ''
			},
			thumb: {
				type: String,
				default: ''
			},
			rightText: {
				type: String,
				default: ''
			},
			disabled: {
				type: Boolean,
				default: false
			},
			clickable: {
				type: Boolean,
				default: false
			},
			showArrow: {
				type: Boolean,
				default: false
			},
			link: {
				type: [Boolean, String],
				default: false,
				validator(value) {
					return !value || ['navigateTo', 'redirectTo', 'reLaunch', 'switchTab'].indexOf(value) !== -1
				}
			},
			to: {
				type: String,
				default: ''
			},
			showBadge: {
				type: Boolean,
				default: false
			},
			badgeText: {
				type: [String, Number],
				default: ''
			},
			badgeType: {
				type: String,
				default: 'success'
			},
			showSwitch: {
				type: Boolean,
				default: false
			},
			switchChecked: {
				type: Boolean,
				default: false
			},
			showExtraIcon: {
				type: Boolean,
				default: false
			},
			extraIcon: {
				type: Object,
				default () {
					return {
						type: '',
						color: '#000000',
						size: 20
					}
				}
			}
		},
		methods: {
			onClick() {
				if (this.disabled) return
				if (this.to !== '') {
					this.openPage()
					return
				}
				this.$emit('click', {
					data: {}
				})
			},
			onSwitchChange(e) {
				this.$emit('switchChange', e.detail)
			},
			openPage() {
				if (['navigateTo', 'redirectTo', 'reLaunch', 'switchTab'].indexOf(this.link) !== -1) {
					uni[this.link]({
						url: this.to
					})
				}
			}
		}
	}
</script>

<style lang="scss">
	$wht-list-item-pd: 12px;

	.wht-list-item {
		position: relative;
		font-size: 16px;
		background-color: #fff;
		flex-direction: column;

		&--disabled {
			opacity: 0.3;
		}

		&--hover {
			background-color: #f1f1f1;
		}

		&__container {
			position: relative;
			display: flex;
			flex-direction: row;
			padding: $wht-list-item-pd;
			padding-left: $wht-list-item-pd;
			flex: 1;
			position: relative;
			justify-content: space-between;
			align-items: center;

			&:after {
				position: absolute;
				z-index: 3;
				right: 0;
				bottom: 0;
				left: $wht-list-item-pd;
				height: 1px;
				content: '';
				-webkit-transform: scaleY(0.5);
				transform: scaleY(0.5);
				background-color: #e5e5e5;
			}
		}

		&__header {
			display: flex;
			flex-direction: row;
			align-items: center;
		}

		&__icon {
			margin-right: $wht-list-item-pd;
			flex-direction: row;
			justify-content: center;
			align-items: center;

			&-img {
				height: 52rpx;
				width: 52rpx;
			}
		}

		&__content {
			flex: 1;
			overflow: hidden;
			display: flex;
			flex-direction: column;

			&-title {
				font-size: 14px;
				color: #3b4144;
				overflow: hidden;
			}

			&-note {
				margin-top: 6rpx;
				color: #999;
				font-size: 12px;
				overflow: hidden;
			}
		}

		&__extra {
			display: flex;
			flex-direction: row;
			justify-content: flex-end;
			align-items: center;

			&-text {
				color: #999;
				font-size: 12px;
				margin-right: 10px;
			}

			&-icon-arrow {
				color: #bbb;
				font-size: 14px;
			}
		}
	}
</style>]]>
