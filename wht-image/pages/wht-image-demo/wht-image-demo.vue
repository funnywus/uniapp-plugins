<template>
  <view class="container">
    <view class="header">
      <text class="header-title">wht-image 图片</text>
      <text class="header-desc">图片组件，支持多种填充模式、加载中、加载失败提示</text>
    </view>

    <view class="section">
      <view class="section-title">基础用法</view>
      <view class="section-content">
        <wht-image
          src="https://img.yzcdn.cn/vant/cat.jpeg"
          width="240"
          height="240"
          :radius="12"
        />
      </view>
    </view>

    <view class="section">
      <view class="section-title">填充模式</view>
      <view class="section-content mode-list">
        <view 
          class="mode-item" 
          v-for="item in modes" 
          :key="item.mode"
        >
          <wht-image
            src="https://img.yzcdn.cn/vant/cat.jpeg"
            width="180"
            height="180"
            :mode="item.mode"
            :radius="8"
          />
          <text class="mode-text">{{ item.text }}</text>
        </view>
      </view>
    </view>

    <view class="section">
      <view class="section-title">圆角展示</view>
      <view class="section-content radius-list">
        <view class="radius-item">
          <wht-image
            src="https://img.yzcdn.cn/vant/cat.jpeg"
            width="180"
            height="180"
            :radius="24"
          />
          <text class="radius-text">圆角</text>
        </view>
        <view class="radius-item">
          <wht-image
            src="https://img.yzcdn.cn/vant/cat.jpeg"
            width="180"
            height="180"
            :radius="90"
          />
          <text class="radius-text">圆形</text>
        </view>
      </view>
    </view>

    <view class="section">
      <view class="section-title">加载中提示</view>
      <view class="section-content loading-list">
        <view class="loading-item">
          <wht-image
            src="https://img.yzcdn.cn/vant/cat.jpeg"
            width="180"
            height="180"
            :radius="8"
          />
          <text class="loading-text">默认提示</text>
        </view>
        <view class="loading-item">
          <wht-image
            src="https://img.yzcdn.cn/vant/cat.jpeg"
            width="180"
            height="180"
            :radius="8"
          >
            <template #loading>
              <view class="custom-loading">
                <view class="custom-loading-icon"></view>
                <text class="custom-loading-text">加载中...</text>
              </view>
            </template>
          </wht-image>
          <text class="loading-text">自定义提示</text>
        </view>
      </view>
    </view>

    <view class="section">
      <view class="section-title">加载失败</view>
      <view class="section-content error-list">
        <view class="error-item">
          <wht-image
            src="https://invalid-url.jpg"
            width="180"
            height="180"
            :radius="8"
          />
          <text class="error-text">默认提示</text>
        </view>
        <view class="error-item">
          <wht-image
            src="https://invalid-url.jpg"
            width="180"
            height="180"
            :radius="8"
          >
            <template #error>
              <view class="custom-error">
                <view class="custom-error-icon"></view>
                <text class="custom-error-text">图片加载失败</text>
              </view>
            </template>
          </wht-image>
          <text class="error-text">自定义提示</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
const modes = [
  { mode: 'aspectFit', text: 'aspectFit' },
  { mode: 'aspectFill', text: 'aspectFill' },
  { mode: 'widthFix', text: 'widthFix' },
  { mode: 'heightFix', text: 'heightFix' }
]
</script>

<style lang="scss" scoped>
.container {
  min-height: 100vh;
  background-color: #f7f8fa;
  padding-bottom: env(safe-area-inset-bottom);
}

.header {
  padding: 44rpx 32rpx;
  background-color: #fff;
  margin-bottom: 24rpx;
  box-shadow: 0 2rpx 8rpx rgba(0, 0, 0, 0.02);
}

.header-title {
  display: block;
  font-size: 40rpx;
  font-weight: 600;
  color: #323233;
  margin-bottom: 16rpx;
}

.header-desc {
  display: block;
  font-size: 28rpx;
  color: #969799;
  line-height: 1.5;
}

.section {
  margin: 24rpx 24rpx 0;
  background-color: #fff;
  border-radius: 16rpx;
  padding: 32rpx;
  box-shadow: 0 2rpx 8rpx rgba(0, 0, 0, 0.02);
}

.section-title {
  font-size: 32rpx;
  font-weight: 600;
  color: #323233;
  margin-bottom: 32rpx;
  padding-left: 16rpx;
  border-left: 8rpx solid #1989fa;
}

.section-content {
  display: flex;
  justify-content: center;
}

.mode-list,
.radius-list,
.loading-list,
.error-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -16rpx;
}

.mode-item,
.radius-item,
.loading-item,
.error-item {
  width: 50%;
  padding: 0 16rpx;
  box-sizing: border-box;
  margin-bottom: 32rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.mode-text,
.radius-text,
.loading-text,
.error-text {
  margin-top: 16rpx;
  font-size: 28rpx;
  color: #646566;
}

.custom-loading {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.custom-loading-icon {
  width: 48rpx;
  height: 48rpx;
  border: 4rpx solid #1989fa;
  border-color: #1989fa transparent transparent transparent;
  border-radius: 50%;
  animation: custom-rotate 1s linear infinite;
  margin-bottom: 16rpx;
}

.custom-loading-text {
  color: #1989fa;
  font-size: 28rpx;
}

.custom-error {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.custom-error-icon {
  width: 80rpx;
  height: 80rpx;
  border: 4rpx solid #ee0a24;
  border-radius: 50%;
  position: relative;
  margin-bottom: 16rpx;

  &::before,
  &::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 40rpx;
    height: 4rpx;
    background-color: #ee0a24;
    transform: translate(-50%, -50%) rotate(45deg);
  }

  &::after {
    transform: translate(-50%, -50%) rotate(-45deg);
  }
}

.custom-error-text {
  color: #ee0a24;
  font-size: 28rpx;
}

@keyframes custom-rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
