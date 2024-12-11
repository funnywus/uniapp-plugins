<template>
  <view class="demo-container">
    <view class="demo-card">
      <view class="demo-card__title">基础用法</view>
      <view class="demo-card__content">
        <wht-race-lamp height="80">
          <text class="basic-text">欢迎使用跑马灯组件！这是一条基础的跑马灯文字效果。</text>
        </wht-race-lamp>
      </view>
    </view>
    
    <view class="demo-card">
      <view class="demo-card__title">不同方向</view>
      <view class="demo-card__content">
        <view class="demo-item">
          <text class="demo-item__label">向左滚动（间距80rpx）</text>
          <wht-race-lamp direction="left" height="80" :speed="50" :gap="80">
            <view class="direction-text">
              <text class="highlight">向左滚动</text>
              <text>这是一条向左滚动的文字，设置了80rpx的间距</text>
            </view>
          </wht-race-lamp>
        </view>
        
        <view class="demo-item">
          <text class="demo-item__label">向右滚动（间距120rpx）</text>
          <wht-race-lamp direction="right" height="80" :speed="50" :gap="120">
            <view class="direction-text">
              <text class="highlight">向右滚动</text>
              <text>这是一条向右滚动的文字，速度为50像素/秒</text>
            </view>
          </wht-race-lamp>
        </view>
        
        <view class="demo-item">
          <text class="demo-item__label">向上滚动（间距40rpx）</text>
          <wht-race-lamp direction="up" height="50" :speed="40" :gap="5">
            <view class="direction-text">
              <text class="highlight">向上滚动</text>
              <text>第一条通知信息</text>
            </view>
          </wht-race-lamp>
        </view>
      </view>
    </view>
    
    <view class="demo-card">
      <view class="demo-card__title">自定义样式</view>
      <view class="demo-card__content">
        <view class="demo-item">
          <text class="demo-item__label">商品促销</text>
          <wht-race-lamp height="80" :gap="100">
            <view class="promo-card">
              <text class="promo-card__tag">限时特惠</text>
              <text class="promo-card__price">¥99.99</text>
              <text class="promo-card__original">原价¥199.99</text>
              <text class="promo-card__desc">新品上市</text>
            </view>
          </wht-race-lamp>
        </view>
        
        <view class="demo-item">
          <text class="demo-item__label">系统通知</text>
          <wht-race-lamp height="80" :gap="60">
            <view class="notice-text">
              <text class="notice-text__tag">通知</text>
              <text>系统将于今晚24:00进行维护升级，预计持续2小时，敬请谅解。</text>
            </view>
          </wht-race-lamp>
        </view>
      </view>
    </view>
  </view>
</template>

<style lang="scss">
.demo-container {
  padding: 30rpx;
  background: linear-gradient(to bottom, #f8f9fc, #f0f2f5);
  min-height: 100vh;
}

.demo-card {
  background: #ffffff;
  border-radius: 20rpx;
  padding: 40rpx;
  margin-bottom: 30rpx;
  box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.05);
  
  &__title {
    font-size: 34rpx;
    font-weight: 600;
    color: #2b2b2b;
    margin-bottom: 30rpx;
    position: relative;
    padding-left: 24rpx;
    
    &::before {
      content: '';
      position: absolute;
      left: 0;
      top: 50%;
      transform: translateY(-50%);
      width: 6rpx;
      height: 32rpx;
      background: linear-gradient(to bottom, #2979ff, #5e96ff);
      border-radius: 6rpx;
    }
  }
}

.demo-item {
  margin-bottom: 40rpx;
  
  &__label {
    font-size: 28rpx;
    color: #666666;
    margin-bottom: 16rpx;
    display: block;
  }
  
  &:last-child {
    margin-bottom: 0;
  }
}

.basic-text {
  color: #2b2b2b;
  font-size: 28rpx;
}

.direction-text {
  display: flex;
  align-items: center;
  gap: 20rpx;
  font-size: 28rpx;
  color: #2b2b2b;
  
  .highlight {
    color: #2979ff;
    font-weight: 500;
  }
}

.promo-card {
  display: flex;
  align-items: center;
  gap: 20rpx;
  
  &__tag {
    background: linear-gradient(to right, #ff4400, #ff6b22);
    color: #ffffff;
    font-size: 24rpx;
    padding: 4rpx 16rpx;
    border-radius: 6rpx;
  }
  
  &__price {
    color: #ff4400;
    font-size: 36rpx;
    font-weight: bold;
  }
  
  &__original {
    color: #999999;
    font-size: 24rpx;
    text-decoration: line-through;
  }
  
  &__desc {
    background: #fff5f0;
    color: #ff4400;
    font-size: 24rpx;
    padding: 4rpx 16rpx;
    border-radius: 6rpx;
  }
}

.notice-text {
  display: flex;
  align-items: center;
  gap: 20rpx;
  font-size: 28rpx;
  color: #2b2b2b;
  
  &__tag {
    background: #e8f3ff;
    color: #2979ff;
    font-size: 24rpx;
    padding: 4rpx 16rpx;
    border-radius: 6rpx;
  }
}
</style> 