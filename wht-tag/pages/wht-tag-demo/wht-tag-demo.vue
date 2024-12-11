<template>
  <view class="container">
    <view class="header">
      <view class="header__title">标签组件</view>
      <view class="header__desc">标签组件用于展示标签信息</view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">基础用法</view>
        </view>
        <view class="section__content">
          <wht-tag>默认标签</wht-tag>
          <wht-tag type="primary">主要标签</wht-tag>
          <wht-tag type="success">成功标签</wht-tag>
          <wht-tag type="warning">警告标签</wht-tag>
          <wht-tag type="error">错误标签</wht-tag>
          <wht-tag type="info">信息标签</wht-tag>
        </view>
      </view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">空心样式</view>
        </view>
        <view class="section__content">
          <wht-tag plain>默认标签</wht-tag>
          <wht-tag type="primary" plain>主要标签</wht-tag>
          <wht-tag type="success" plain>成功标签</wht-tag>
          <wht-tag type="warning" plain>警告标签</wht-tag>
          <wht-tag type="error" plain>错误标签</wht-tag>
          <wht-tag type="info" plain>信息标签</wht-tag>
        </view>
      </view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">圆角样式</view>
        </view>
        <view class="section__content">
          <wht-tag round>默认标签</wht-tag>
          <wht-tag type="primary" round>主要标签</wht-tag>
          <wht-tag type="success" round>成功标签</wht-tag>
        </view>
      </view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">标记样式</view>
        </view>
        <view class="section__content">
          <wht-tag mark>默认标签</wht-tag>
          <wht-tag type="primary" mark>主要标签</wht-tag>
          <wht-tag type="success" mark>成功标签</wht-tag>
        </view>
      </view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">可关闭</view>
        </view>
        <view class="section__content">
          <wht-tag v-for="(tag, index) in closableTags" 
                   :key="index" 
                   :type="tag.type" 
                   closeable 
                   @close="onClose(index)">
            {{tag.text}}
          </wht-tag>
        </view>
      </view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">渐变颜色</view>
          <view class="section__desc">支持渐变背景和渐变边框效果</view>
        </view>
        <view class="section__content">
          <wht-tag v-for="(tag, index) in gradientTags" 
                   :key="'filled-' + index"
                   :gradient="tag.gradient"
                   :text-color="tag.textColor"
                   round>
            {{tag.text}}
          </wht-tag>
        </view>
      </view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">自定义颜色</view>
        </view>
        <view class="section__content">
          <wht-tag color="#f50">自定义颜色</wht-tag>
          <wht-tag color="#f50" plain>自定义颜色</wht-tag>
          <wht-tag color="#f50" text-color="#fff">自定义文字颜色</wht-tag>
        </view>
      </view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">迷你尺寸</view>
        </view>
        <view class="section__content">
          <wht-tag size="mini">迷你标签</wht-tag>
          <wht-tag type="primary" size="mini">迷你标签</wht-tag>
          <wht-tag type="success" size="mini">迷你标签</wht-tag>
        </view>
      </view>
    </view>
    
    <view class="section">
      <view class="section__card">
        <view class="section__header">
          <view class="section__title">禁用状态</view>
        </view>
        <view class="section__content">
          <wht-tag disabled>禁用标签</wht-tag>
          <wht-tag type="primary" disabled>禁用标签</wht-tag>
          <wht-tag type="success" disabled>禁用标签</wht-tag>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      closableTags: [
        { type: 'default', text: '默认标签' },
        { type: 'primary', text: '主要标签' },
        { type: 'success', text: '成功标签' }
      ],
      gradientTags: [
        { 
          gradient: 'linear-gradient(45deg, #4facfe 0%, #00f2fe 100%)',
          textColor: '#ffffff',
          text: '清新蓝'
        },
        { 
          gradient: 'linear-gradient(45deg, #ff9a9e 0%, #fad0c4 100%)',
          textColor: '#666666',
          text: '温柔粉'
        },
        { 
          gradient: 'linear-gradient(45deg, #43e97b 0%, #38f9d7 100%)',
          textColor: '#ffffff',
          text: '薄荷绿'
        },
        { 
          gradient: 'linear-gradient(45deg, #fa709a 0%, #fee140 100%)',
          textColor: '#ffffff',
          text: '粉黄'
        },
        { 
          gradient: 'linear-gradient(45deg, #a18cd1 0%, #fbc2eb 100%)',
          textColor: '#ffffff',
          text: '梦幻紫'
        }
      ]
    }
  },
  methods: {
    onClose(index) {
      this.closableTags.splice(index, 1)
      uni.showToast({
        title: '标签已删除',
        icon: 'none'
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  padding: 24rpx;
  background-color: #f5f5f5;
  min-height: 100vh;
}

.header {
  margin-bottom: 24rpx;
  
  &__title {
    font-size: 36rpx;
    font-weight: 600;
    color: #333;
    margin-bottom: 8rpx;
  }
  
  &__desc {
    font-size: 28rpx;
    color: #666;
  }
}

.section {
  margin-bottom: 24rpx;
  
  &__card {
    background-color: #fff;
    border-radius: 12rpx;
    padding: 24rpx;
    box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.04);
  }
  
  &__header {
    margin-bottom: 24rpx;
  }
  
  &__title {
    font-size: 32rpx;
    font-weight: 500;
    color: #333;
    margin-bottom: 8rpx;
  }
  
  &__desc {
    font-size: 26rpx;
    color: #666;
    line-height: 1.5;
  }
  
  &__content {
    display: flex;
    flex-wrap: wrap;
    gap: 16rpx;
    
    .wht-tag {
      margin-bottom: 8rpx;
    }
  }
}
</style>
