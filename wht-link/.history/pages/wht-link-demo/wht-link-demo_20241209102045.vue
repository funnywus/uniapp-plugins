<template>
  <view class="container">
    <view class="header">
      <text class="title">wht-link 链接组件</text>
      <text class="description">文字链接的基础组件，支持多种样式和交互方式</text>
    </view>

    <view class="section">
      <view class="section-title">基础用法</view>
      <view class="section-desc">支持多种类型的链接样式，可根据场景选择</view>
      <view class="demo-group">
        <view class="demo-item">
          <wht-link text="默认链接"></wht-link>
        </view>
        <view class="demo-item">
          <wht-link type="primary" text="主要链接"></wht-link>
        </view>
        <view class="demo-item">
          <wht-link type="success" text="成功链接"></wht-link>
        </view>
        <view class="demo-item">
          <wht-link type="warning" text="警告链接"></wht-link>
        </view>
        <view class="demo-item">
          <wht-link type="danger" text="危险链接"></wht-link>
        </view>
        <view class="demo-item">
          <wht-link type="info" text="信息链接"></wht-link>
        </view>
      </view>
    </view>

    <view class="section">
      <view class="section-title">禁用状态</view>
      <view class="section-desc">通过 disabled 属性禁用链接</view>
      <view class="demo-group">
        <view class="demo-item">
          <wht-link disabled text="禁用链接"></wht-link>
        </view>
      </view>
    </view>

    <view class="section">
      <view class="section-title">下划线</view>
      <view class="section-desc">通过 underline 属性控制下划线的显示</view>
      <view class="demo-group">
        <view class="demo-item">
          <wht-link :underline="false" text="无下划线"></wht-link>
        </view>
        <view class="demo-item">
          <wht-link text="有下划线"></wht-link>
        </view>
      </view>
    </view>

    <view class="section">
      <view class="section-title">高级用法</view>
      <view class="section-desc">支持链接跳转、复制和自定义样式</view>
      <view class="demo-group">
        <view class="demo-item">
          <view class="demo-item-title">链接跳转/复制</view>
          <wht-link href="https://www.example.com" text="点击跳转链接 (小程序中自动复制)"></wht-link>
        </view>
        <view class="demo-item">
          <view class="demo-item-title">下载链接（仅H5平台）</view>
          <view class="demo-row">
            <wht-link 
              href="http://jsrelease-file.yunmaster.cn/store/pack/jmb_project_audit/jmb_device_box_2.3.3.apk" 
              :download="true"
              text="直接下载">
            </wht-link>
          </view>
          <view class="demo-row">
            <wht-link 
              href="http://jsrelease-file.yunmaster.cn/store/pack/jmb_project_audit/jmb_device_box_2.3.3.apk" 
              :download="true"
              filename="自定义文件名.apk"
              text="自定义文件名下载">
            </wht-link>
          </view>
          <view class="demo-tip">在H5平台点击时会触发下载，其他平台会正常打开链接</view>
        </view>
        <view class="demo-item">
          <view class="demo-item-title">点击事件</view>
          <wht-link @click="handleClick" text="带点击事件"></wht-link>
        </view>
        <view class="demo-item">
          <view class="demo-item-title">图标链接</view>
          <wht-link>
            <template #prefix>
              <text class="prefix-icon">🔗</text>
            </template>
            带图标的链接
          </wht-link>
        </view>
        <view class="demo-item">
          <view class="demo-item-title">自定义样式</view>
          <wht-link :customStyle="{ fontSize: '32rpx', fontWeight: 'bold' }" text="自定义样式"></wht-link>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
const handleClick = () => {
  uni.showToast({
    title: '点击了链接',
    icon: 'none'
  })
}
</script>

<style lang="scss" scoped>
.container {
  padding: 30rpx;
  background-color: #f5f7fa;
  min-height: 100vh;
}

.header {
  margin-bottom: 40rpx;
  padding: 40rpx;
  background: linear-gradient(135deg, #409eff 0%, #64b5f6 100%);
  border-radius: 16rpx;
  color: #fff;
  
  .title {
    font-size: 40rpx;
    font-weight: 600;
    margin-bottom: 16rpx;
    display: block;
  }
  
  .description {
    font-size: 28rpx;
    opacity: 0.9;
  }
}

.section {
  margin-bottom: 40rpx;
  background-color: #fff;
  border-radius: 16rpx;
  padding: 30rpx;
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.05);
}

.section-title {
  font-size: 32rpx;
  font-weight: 600;
  margin-bottom: 16rpx;
  color: #2c3e50;
  position: relative;
  padding-left: 24rpx;
  
  &::before {
    content: '';
    position: absolute;
    left: 0;
    top: 50%;
    transform: translateY(-50%);
    width: 6rpx;
    height: 28rpx;
    background: #409eff;
    border-radius: 3rpx;
  }
}

.section-desc {
  font-size: 26rpx;
  color: #909399;
  margin-bottom: 24rpx;
}

.demo-group {
  background-color: #f8f9fb;
  border-radius: 8rpx;
  padding: 24rpx;
}

.demo-item {
  margin: 20rpx 0;
  
  &:first-child {
    margin-top: 0;
  }
  
  &:last-child {
    margin-bottom: 0;
  }
}

.demo-item-title {
  font-size: 26rpx;
  color: #606266;
  margin-bottom: 12rpx;
}

.prefix-icon {
  margin-right: 10rpx;
}

.demo-tip {
  font-size: 24rpx;
  color: #909399;
  margin-top: 8rpx;
  font-style: italic;
}

.demo-row {
  margin: 12rpx 0;
  
  &:first-child {
    margin-top: 0;
  }
  
  &:last-child {
    margin-bottom: 0;
  }
}

// 添加响应式布局
@media screen and (min-width: 768px) {
  .container {
    max-width: 1200rpx;
    margin: 0 auto;
  }
  
  .section {
    margin: 40rpx auto;
  }
}
</style>
