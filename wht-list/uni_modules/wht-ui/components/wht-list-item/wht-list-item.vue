<template>
	<view 
		class="wht-list-item"
		:class="{
			'wht-list-item--disabled': disabled,
			'wht-list-item--hover': !disabled && (clickable || link),
		}"
		:hover-class="(!disabled && (clickable || link)) ? 'wht-list-item--hover-active' : ''"
		@click="onClick"
	>
		<!-- 左侧图标/图片 -->
		<view class="wht-list-item__header" v-if="thumb || showExtraIcon || $slots.header">
			<slot name="header">
				<image v-if="thumb" :src="thumb" class="wht-list-item__thumb" />
				<uni-icons v-if="showExtraIcon" :type="extraIcon.type" :color="extraIcon.color" :size="extraIcon.size" />
			</slot>
		</view>
		
		<!-- 主要内容 -->
		<view class="wht-list-item__content">
			<view class="wht-list-item__title">
				<text :class="{'wht-list-item__title-text': true}">{{ title }}</text>
				<text v-if="note" class="wht-list-item__note">{{ note }}</text>
			</view>
		</view>
		
		<!-- 右侧内容 -->
		<view class="wht-list-item__right">
			<slot name="right">
				<text v-if="rightText" class="wht-list-item__right-text">{{ rightText }}</text>
				<view v-if="showBadge" class="wht-list-item__badge">
					<uni-badge :text="badgeText" :type="badgeType" />
				</view>
				<switch 
					v-if="showSwitch" 
					:disabled="disabled" 
					:checked="switchChecked"
					@change="onSwitchChange" 
				/>
				<uni-icons v-if="showArrow" type="right" size="16" color="#bbb" />
			</slot>
		</view>
	</view>
</template>

<script>
	/**
	 * ListItem 列表子组件
	 * @description 列表子组件，可单独使用，也可以搭配wht-list组件使用
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
		data() {
			return {
				isFirstChild: false
			}
		},
		mounted() {
			this.list = this.getForm()
			if (this.list) {
				if (!this.list.firstChildAppend) {
					this.list.firstChildAppend = true
					this.isFirstChild = true
				}
			}
		},
		methods: {
			/**
			 * 获取父元素实例
			 */
			getForm(name = 'wht-list') {
				let parent = this.$parent;
				let parentName = parent.$options.name;
				while (parentName !== name) {
					if (parentName === 'wht-list') return parent;
					parent = parent.$parent
					if (!parent) return false
					parentName = parent.$options.name
				}
				return parent;
			},
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

<style lang="scss" scoped>

.wht-list-item {
	position: relative;
	display: flex;
	flex-direction: row;
	align-items: center;
	padding: $wht-list-item-padding;
	font-size: $wht-list-item-font-size;
	line-height: $wht-list-item-line-height;
	background-color: $wht-list-bg-color;
	
	&:not(:last-child)::after {
		content: '';
		position: absolute;
		left: 15px;
		right: 0;
		bottom: 0;
		height: 1px;
		transform: scaleY(0.5);
		background-color: $wht-list-border-color;
	}
	
	&--hover {
		cursor: pointer;
	}
	
	&--hover-active {
		background-color: $wht-list-item-hover-bg;
	}
	
	&--disabled {
		opacity: $wht-list-item-disabled-opacity;
		cursor: not-allowed;
	}
	
	&__header {
		margin-right: 12px;
	}
	
	&__thumb {
		width: 36px;
		height: 36px;
		border-radius: 4px;
	}
	
	&__content {
		flex: 1;
		overflow: hidden;
	}
	
	&__title {
		&-text {
			color: $wht-list-item-color;
		}
	}
	
	&__note {
		display: block;
		margin-top: 4px;
		color: $wht-list-item-note-color;
		font-size: $wht-list-item-note-font-size;
	}
	
	&__right {
		display: flex;
		align-items: center;
		margin-left: 12px;
		
		&-text {
			margin-right: 4px;
			color: $wht-list-item-note-color;
			font-size: $wht-list-item-note-font-size;
		}
	}
}
</style>