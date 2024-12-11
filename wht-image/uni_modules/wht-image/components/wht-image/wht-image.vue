<template>
  <view class="wht-image" :style="[wrapStyle]" @click="onClick">
    <image
      :src="src"
      :mode="mode"
      :lazy-load="lazyLoad"
      :show-menu-by-longpress="showMenuByLongpress"
      :style="[imageStyle]"
      @error="onError"
      @load="onLoad"
    />
    <view v-if="showLoading && loading" class="wht-image__loading">
      <slot name="loading">
        <view class="wht-image__loading-spinner">
          <view class="wht-image__loading-dot"></view>
          <view class="wht-image__loading-dot"></view>
          <view class="wht-image__loading-dot"></view>
        </view>
      </slot>
    </view>
    <view v-if="showError && isError" class="wht-image__error">
      <slot name="error">
        <view class="wht-image__error-content">
          <view class="wht-image__error-icon">
            <view class="wht-image__error-line"></view>
            <view class="wht-image__error-line"></view>
          </view>
          <text class="wht-image__error-text">图片加载失败</text>
          <text class="wht-image__error-tip">点击重试</text>
        </view>
      </slot>
    </view>
  </view>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  // 图片链接
  src: {
    type: String,
    default: ''
  },
  // 图片裁剪、缩放的模式
  mode: {
    type: String,
    default: 'aspectFill'
  },
  // 宽度，单位rpx
  width: {
    type: [String, Number],
    default: '100%'
  },
  // 高度，单位rpx
  height: {
    type: [String, Number],
    default: '100%'
  },
  // 圆角，单位rpx
  radius: {
    type: [String, Number],
    default: 0
  },
  // 是否懒加载
  lazyLoad: {
    type: Boolean,
    default: true
  },
  // 长按图片显示发送给朋友、收藏、保存图片、搜一搜、打开名片/前往群聊界面菜单
  showMenuByLongpress: {
    type: Boolean,
    default: true
  },
  // 是否显示加载中
  showLoading: {
    type: Boolean,
    default: true
  },
  // 是否显示加载失败
  showError: {
    type: Boolean,
    default: true
  },
  // 背景颜色
  bgColor: {
    type: String,
    default: '#f3f4f6'
  }
})

const emit = defineEmits(['click', 'error', 'load'])

const loading = ref(true)
const isError = ref(false)

// 包装样式
const wrapStyle = computed(() => {
  const style = {}
  if (props.width) style.width = isNaN(props.width) ? props.width : `${props.width}rpx`
  if (props.height) style.height = isNaN(props.height) ? props.height : `${props.height}rpx`
  if (props.radius) style.borderRadius = isNaN(props.radius) ? props.radius : `${props.radius}rpx`
  if (props.bgColor) style.backgroundColor = props.bgColor
  return style
})

// 图片样式
const imageStyle = computed(() => {
  return {
    opacity: loading.value || isError.value ? 0 : 1
  }
})

// 点击事件
const onClick = () => {
  emit('click')
}

// 加载失败
const onError = () => {
  isError.value = true
  loading.value = false
  emit('error')
}

// 加载完成
const onLoad = () => {
  loading.value = false
  isError.value = false
  emit('load')
}
</script>

<style lang="scss" scoped>
.wht-image {
  position: relative;
  overflow: hidden;

  image {
    width: 100%;
    height: 100%;
    transition: opacity 0.3s ease;
  }

  &__loading,
  &__error {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #f7f8fa;
  }

  &__loading-spinner {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8rpx;
  }

  &__loading-dot {
    width: 16rpx;
    height: 16rpx;
    background-color: #1989fa;
    border-radius: 50%;
    animation: dot-bounce 0.8s infinite;

    &:nth-child(2) {
      animation-delay: 0.2s;
    }

    &:nth-child(3) {
      animation-delay: 0.4s;
    }
  }

  &__error-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 24rpx;
    border-radius: 16rpx;
    background: rgba(255, 255, 255, 0.9);
    backdrop-filter: blur(8rpx);
    box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.1);
  }

  &__error-icon {
    width: 80rpx;
    height: 80rpx;
    border: 4rpx solid #ff4646;
    border-radius: 50%;
    position: relative;
    margin-bottom: 16rpx;
    transform: rotate(45deg);
    animation: error-rotate 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }

  &__error-line {
    position: absolute;
    background-color: #ff4646;
    border-radius: 4rpx;

    &:first-child {
      width: 40rpx;
      height: 4rpx;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    &:last-child {
      width: 4rpx;
      height: 40rpx;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }

  &__error-text {
    font-size: 28rpx;
    color: #323233;
    margin-bottom: 8rpx;
  }

  &__error-tip {
    font-size: 24rpx;
    color: #909399;
  }
}

@keyframes dot-bounce {
  0%, 80%, 100% {
    transform: scale(0.8);
    opacity: 0.5;
  }
  40% {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes error-rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(45deg);
  }
}
</style>
