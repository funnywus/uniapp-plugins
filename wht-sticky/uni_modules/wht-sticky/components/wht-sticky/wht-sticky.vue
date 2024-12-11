<template>
  <view class="wht-sticky-container">
    <view class="wht-sticky-placeholder" v-if="isFixed" :style="{ height: contentHeight + 'px' }"></view>
    <view 
      class="wht-sticky-content" 
      :class="{ 'wht-sticky-fixed': isFixed }"
      :style="stickyStyle"
      ref="stickyEl"
    >
      <slot></slot>
    </view>
  </view>
</template>

<script>
export default {
  name: 'wht-sticky',
  props: {
    offsetTop: {
      type: Number,
      default: 0
    },
    zIndex: {
      type: Number,
      default: 99
    }
  },
  data() {
    return {
      isFixed: false,
      contentHeight: 0,
      observer: null,
      originalTop: 0
    }
  },
  computed: {
    stickyStyle() {
      if (!this.isFixed) return {}
      return {
        position: 'fixed',
        top: this.offsetTop + 'px',
        zIndex: this.zIndex,
        width: '100%'
      }
    }
  },
  mounted() {
    setTimeout(() => {
      this.init()
    }, 20)
  },
  beforeDestroy() {
    this.destroy()
  },
  beforeUnmount() {
    this.destroy()
  },
  methods: {
    init() {
      const query = uni.createSelectorQuery().in(this)
      query.select('.wht-sticky-content').boundingClientRect(data => {
        if (data) {
          this.contentHeight = data.height
          this.originalTop = data.top
          this.initObserver()
        }
      }).exec()
    },
    initObserver() {
      try {
        if (this.observer) {
          this.observer.disconnect()
        }
        
        this.observer = uni.createIntersectionObserver(this)
        this.observer.relativeToViewport({
          top: -this.offsetTop
        }).observe('.wht-sticky-content', (res) => {
          const { boundingClientRect, intersectionRatio } = res
          
          // 元素完全离开视口时取消吸顶
          if (!intersectionRatio) {
            this.isFixed = false
            return
          }
          
          // 当元素距离顶部小于等于预设值时吸顶
          if (boundingClientRect.top <= this.offsetTop) {
            this.isFixed = true
          } else {
            // 当元素距离顶部大于预设值时取消吸顶
            this.isFixed = false
          }
        })
      } catch (e) {
        console.error('初始化吸顶组件失败:', e)
      }
    },
    destroy() {
      if (this.observer) {
        this.observer.disconnect()
        this.observer = null
      }
    }
  },
  watch: {
    offsetTop: {
      handler() {
        if (this.observer) {
          this.destroy()
          setTimeout(() => {
            this.init()
          }, 20)
        }
      }
    }
  }
}
</script>

<style scoped>
.wht-sticky-container {
  position: relative;
}
.wht-sticky-content {
  width: 100%;
}
.wht-sticky-fixed {
  position: fixed;
  left: 0;
  right: 0;
}
.wht-sticky-placeholder {
  width: 100%;
}
</style>
