## wht-tabbar 自定义凸起tabbar
> **组件名：wht-tabbar**
> 代码块： `wht-tabbar`


### 插件代码
```
<template>
    <view class="wht-tabbar" :style="{ height: height + 'rpx' }">
        <view v-for="(item, index) in list" :key="index" class="tabbar-item" :class="[
            index === centerIndex ? 'center-item' : '',
            current === index ? 'active' : ''
        ]" @click="onClick(index)">
            <view class="icon-box" :class="{ 'center-icon': index === centerIndex }">
                <image :src="current === index ? item.selectedIconPath : item.iconPath" class="tabbar-icon"
                    :class="{ 'bigger': index === centerIndex }"></image>
            </view>
            <text class="tabbar-text" v-if="item.text">{{ item.text }}</text>
        </view>
    </view>
</template>

<script>
// #ifdef VUE3
import { defineComponent } from 'vue'
export default defineComponent({
    // #endif

    // #ifdef VUE2
    export default {
        // #endif
        name: 'wht-tabbar',
        props: {
            height: {
                type: Number,
                default: 120
            },
            current: {
                type: Number,
                default: 0
            },
            centerIndex: {
                type: Number,
                default: 2
            },
            list: {
                type: Array,
                default: () => ([
                    {
                        text: '首页',
                        iconPath: '/static/images/tabbar/home.png',
                        selectedIconPath: '/static/images/tabbar/home_.png'
                    },
                    {
                        text: '发现',
                        iconPath: '/static/images/tabbar/find.png',
                        selectedIconPath: '/static/images/tabbar/find_.png'
                    },
                    {
                        text: '',
                        iconPath: '/static/images/tabbar/plus.png',
                        selectedIconPath: '/static/images/tabbar/plus.png'
                    },
                    {
                        text: '消息',
                        iconPath: '/static/images/tabbar/msg.png',
                        selectedIconPath: '/static/images/tabbar/msg_.png'
                    },
                    {
                        text: '我的',
                        iconPath: '/static/images/tabbar/my.png',
                        selectedIconPath: '/static/images/tabbar/my_.png'
                    }
                ])
            }
        },
        emits: ['update:current', 'click', 'publish'],

        // #ifdef VUE3
        setup(props, { emit }) {
            const onClick = (index) => {
                if (index === props.centerIndex) {
                    emit('click', index)
                    return
                }
                emit('update:current', index)
                emit('click', index)
            }

            return {
                onClick
            }
        }
  // #endif

  // #ifdef VUE2
  methods: {
            onClick(index) {
                if (index === this.centerIndex) {
                    // 发布按钮点击
                    this.$emit('click', index)
                    return
                }
                this.$emit('update:current', index)
                this.$emit('click', index)
            }
        }
        // #endif
    })
</script>

<style lang="scss" scoped>
.wht-tabbar {
    width: 100%;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: #ffffff;
    display: flex;
    justify-content: space-around;
    align-items: flex-end;
    box-shadow: 0 -1px 5px rgba(0, 0, 0, 0.1);
    padding-bottom: env(safe-area-inset-bottom);
    height: 120rpx;

    .tabbar-item {
        flex: 1;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 12rpx 0;
        position: relative;

        &.center-item {
            margin-top: -60rpx;

            &::after {
                content: '';
                position: absolute;
                top: -40rpx;
                left: 50%;
                transform: translateX(-50%);
                width: 120rpx;
                height: 60rpx;
                box-shadow: 0 -1px 5px rgba(0, 0, 0, 0.1);
                background-color: #fff;
                border-radius: 120rpx 120rpx 0 0;
                z-index: -1;
            }

            .icon-box {
                position: relative;
                z-index: 1;
                top: -30rpx;
            }
        }

        .icon-box {
            width: 96rpx;
            // height: 96rpx;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 6rpx;
        }

        .tabbar-icon {
            width: 44rpx;
            height: 44rpx;

            &.bigger {
                width: 76rpx;
                height: 76rpx;
            }
        }

        .tabbar-text {
            font-size: 24rpx;
            color: #666;
            line-height: 1;
        }

        &.active {
            .tabbar-text {
                color: #007AFF;
            }
        }
    }
}
</style>
```


### 使用方法
```
<template>
	<view class="container">
		<view class="content" v-if="currentTab === 0">
			<text class="title">首页</text>
		</view>
		<view class="content" v-if="currentTab === 1">
			<text class="title">发现</text>
		</view>
		<view class="content" v-if="currentTab === 2">
			<text class="title">发布</text>
		</view>
		<view class="content" v-if="currentTab === 3">
			<text class="title">消息</text>
		</view>
		<view class="content" v-if="currentTab === 4">
			<text class="title">我的</text>
		</view>
		<wht-tabbar v-model:current="currentTab" :centerIndex="2" @click="handleTabClick" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				currentTab: 0
			}
		},
		methods: {
			handleTabClick(index) {
				console.log('handleTabClick index ', index)
				if (index === 2) {
					// 发布按钮点击
					// 可做弹窗
					uni.showToast({
						title: "凸起"
					})
					return
				}
				this.currentTab = index
			}
		}
	}
</script>

<style>
	.container {
		min-height: 100vh;
		padding-bottom: 100rpx;
	}

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
</style>
```