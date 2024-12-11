<template>
  <view class="category-container">
    <!-- 左侧分类列表 -->
    <scroll-view 
      class="category-menu" 
      scroll-y 
      :scroll-top="leftScrollTop"
      :scroll-with-animation="true"
    >
      <view class="menu-list">
        <view 
          v-for="(item, index) in tabList" 
          :key="index"
          class="menu-item"
          :class="{ active: currentTab === index }"
          @click="handleTabClick(index)"
        >
          <image 
            v-if="item.icon" 
            class="menu-icon" 
            :src="item.icon" 
            mode="aspectFit"
          ></image>
          <text class="menu-name">{{ item.name }}</text>
        </view>
      </view>
    </scroll-view>
    
    <!-- 右侧商品内容区 -->
    <scroll-view 
      class="goods-content" 
      scroll-y 
      :scroll-top="rightScrollTop"
      :scroll-with-animation="true"
      @scroll="handleContentScroll"
    >
      <view 
        class="category-section"
        v-for="(item, index) in tabList"
        :key="index"
        :id="`category_${index}`"
      >
        <!-- 分类广告图 -->
        <image 
          v-if="item.banner" 
          class="category-banner" 
          :src="item.banner" 
          mode="widthFix"
        ></image>
        
        <!-- 分类标题 -->
        <view class="section-title">
          <text class="title-text">{{item.name}}</text>
          <text v-if="item.desc" class="title-desc">{{item.desc}}</text>
        </view>
        
        <!-- 分类内容插槽 -->
        <slot :name="`content_${index}`"></slot>
      </view>
    </scroll-view>
  </view>
</template>

<script>
export default {
  name: 'wht-v-tabs',
  props: {
    tabList: {
      type: Array,
      default: () => []
    },
    defaultIndex: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      currentTab: this.defaultIndex,
      leftScrollTop: 0,
      rightScrollTop: 0,
      contentPositions: [],
      scrolling: false,
      timer: null
    }
  },
  mounted() {
    setTimeout(() => {
      this.initContentPositions()
    }, 200)
  },
  methods: {
    async initContentPositions() {
      const query = uni.createSelectorQuery().in(this)
      this.contentPositions = []
      
      for(let i = 0; i < this.tabList.length; i++) {
        await new Promise(resolve => {
          query.select(`#category_${i}`).boundingClientRect(rect => {
            if(rect) {
              this.contentPositions.push({
                top: rect.top,
                bottom: rect.bottom,
                height: rect.height
              })
            }
            resolve()
          }).exec()
        })
      }
    },
    
    handleTabClick(index) {
      if(this.currentTab === index) return
      this.scrolling = true
      this.currentTab = index
      
      const targetTop = this.contentPositions[index]?.top || 0
      this.rightScrollTop = targetTop
      
      this.leftScrollTop = Math.max(0, index * 84 - 200)
      // 左侧选项卡滚动位置
      this.leftScrollTop = Math.max(0, index * 100 - 200)
      
      this.$emit('change', index)
      
      // 防止滚动期间触发scroll事件导致判断错误
      clearTimeout(this.timer)
      this.timer = setTimeout(() => {
        this.scrolling = false
      }, 300)
    },
    
    handleContentScroll(e) {
      if(this.scrolling) return
      
      const scrollTop = e.detail.scrollTop
      const viewHeight = e.detail.scrollHeight - e.detail.scrollTop
      
      // 找到当前显示的内容块
      let activeIndex = 0
      this.contentPositions.forEach((pos, index) => {
        const offsetTop = pos.top - scrollTop
        if(offsetTop <= viewHeight / 3) {
          activeIndex = index
        }
      })
      
      if(this.currentTab !== activeIndex) {
        this.currentTab = activeIndex
        // 同步左侧选项卡位置
        this.leftScrollTop = Math.max(0, activeIndex * 100 - 200)
        this.$emit('change', activeIndex)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.wht-v-tabs {
  display: flex;
  width: 100%;
  height: 100%;
  background: #fff;
  
  .tabs-scroll {
    width: 180rpx;
    height: 100%;
    background: #f8f8f8;
  }
  
  .tabs-bar {
    padding: 20rpx 0;
  }
  
  .tab-item {
    position: relative;
    padding: 30rpx 20rpx;
    text-align: left;
    transition: all 0.3s;
    font-size: 28rpx;
    color: #666;
    
    .tab-badge {
      margin-left: 10rpx;
      font-size: 24rpx;
      color: #999;
    }
    
    &.active {
      background: #fff;
      color: #2979ff;
      font-weight: bold;
      
      &::before {
        content: '';
        position: absolute;
        left: 0;
        top: 50%;
        transform: translateY(-50%);
        height: 32rpx;
        width: 8rpx;
        background: #2979ff;
        border-radius: 0 4rpx 4rpx 0;
      }
      
      .tab-badge {
        color: #2979ff;
      }
    }
  }
  
  .content-wrap {
    flex: 1;
    height: 100%;
  }
  
  .content-item {
    padding: 20rpx;
    
    .item-title {
      font-size: 32rpx;
      font-weight: bold;
      margin-bottom: 20rpx;
      color: #333;
    }
  }
}
</style>
