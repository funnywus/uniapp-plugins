<!-- 
 * @description 跑马灯组件 - 支持水平和垂直方向的文字滚动效果
 * @property {String} direction 滚动方向 - 可选值：left/right/up/down
 * @property {Number} speed 滚动速度，默认60
 * @property {Number} delay 开始滚动的延迟时间，默认0
 * @property {String/Number} height 容器高度，默认80
 * @property {Boolean} autoplay 是否自动播放，默认true
 * @property {String/Number} gap 内容间隔，默认0
 * @example 
 *  <wht-race-lamp direction="left" height="80" :speed="50" :gap="80">
 *    <text>跑马灯文字内容</text>
 *  </wht-race-lamp>
 -->

<template>
  <view class="wht-race-lamp" :style="containerStyle">
    <view class="wht-race-lamp__wrapper" :class="[direction]" :style="wrapperStyle" @touchstart="onTouchStart"
      @touchend="onTouchEnd">
      <view class="wht-race-lamp__content">
        <slot></slot>
      </view>
      <view class="wht-race-lamp__content">
        <slot></slot>
      </view>
      <view class="wht-race-lamp__content">
        <slot></slot>
      </view>
      <view class="wht-race-lamp__content">
        <slot></slot>
      </view>
      <view class="wht-race-lamp__content">
        <slot></slot>
      </view>
    </view>
  </view>
</template>

<script>
/**
 * wht-race-lamp 跑马灯组件
 * @description 支持水平和垂直方向的文字滚动效果
 */
export default {
  name: 'wht-race-lamp',
  props: {
    direction: {
      type: String,
      default: 'left',
      validator: (value) => ['left', 'right', 'up', 'down'].includes(value)
    },
    speed: {
      type: Number,
      default: 60
    },
    delay: {
      type: Number,
      default: 0
    },
    height: {
      type: [String, Number],
      default: 80
    },
    autoplay: {
      type: Boolean,
      default: true
    },
    gap: {
      type: [String, Number],
      default: 0
    }
  },
  data() {
    return {
      isRunning: false,
      offset: 0,
      contentSize: 0,
      containerSize: 0,
      animationId: null,
      lastTimestamp: 0
    }
  },
  computed: {
    containerStyle() {
      return {
        height: typeof this.height === 'number' ? this.height + 'rpx' : this.height
      }
    },
    wrapperStyle() {
      const transform = this.isVertical
        ? `translateY(${this.offset}px)`
        : `translateX(${this.offset}px)`

      return {
        transform,
        transition: this.isRunning ? 'none' : 'transform 0.3s'
      }
    },
    isVertical() {
      return ['up', 'down'].includes(this.direction)
    }
  },
  mounted() {
    this.$nextTick(() => {
      setTimeout(() => {
        this.initSize()
        if (this.autoplay) {
          setTimeout(() => {
            this.start()
          }, this.delay * 1000)
        }
      }, 100)
    })
  },
  beforeDestroy() {
    this.stop()
  },
  methods: {
    async initSize() {
      const query = uni.createSelectorQuery().in(this)
      query.select('.wht-race-lamp__content').boundingClientRect(data => {
        if (!data) return

        if (this.isVertical) {
          // 计算内容高度加上间距
          const gapSize = this.gap ? (typeof this.gap === 'number' ? this.gap : parseFloat(this.gap)) : 0
          this.contentSize = data.height + (gapSize || 0)
          this.offset = this.direction === 'down' ? -this.contentSize * 2 : -this.contentSize
        } else {
          this.contentSize = data.width
          this.offset = this.direction === 'right' ? -this.contentSize * 2 : -this.contentSize
        }
      }).exec()
    },
    start() {
      if (this.isRunning) return
      this.isRunning = true
      this.lastTimestamp = Date.now()
      this.animate()
    },
    stop() {
      this.isRunning = false
      if (this.animationId) {
        clearTimeout(this.animationId)
        this.animationId = null
      }
    },
    animate() {
      if (!this.isRunning) return

      const now = Date.now()
      const deltaTime = now - this.lastTimestamp
      const step = (this.speed * deltaTime) / 1000

      let newOffset = this.offset

      if (['left', 'up'].includes(this.direction)) {
        newOffset -= step
        if (Math.abs(newOffset) >= this.contentSize * 3) {
          newOffset = -this.contentSize
        }
      } else {
        newOffset += step
        if (newOffset >= -this.contentSize) {
          newOffset = -this.contentSize * 3
        }
      }

      this.offset = newOffset
      this.lastTimestamp = now

      this.animationId = setTimeout(() => {
        this.animate()
      }, 16)
    },
    onTouchStart() {
      this.stop()
    },
    onTouchEnd() {
      if (this.autoplay) {
        this.start()
      }
    }
  }
}
</script>

<style lang="scss">
.wht-race-lamp {
  position: relative;
  width: 100%;
  overflow: hidden;
  height: 80rpx;

  &__wrapper {
    position: relative;
    height: 100%;
    will-change: transform;
    display: flex;
    align-items: center;

    &.up,
    &.down {
      flex-direction: column;

      .wht-race-lamp__content {
        margin-bottom: v-bind('typeof gap === "number" ? gap + "rpx" : gap');


        &:last-child {
          margin-right: 0;
        }
      }
    }

    &.left,
    &.right {
      flex-direction: row;

      .wht-race-lamp__content {
        margin-right: v-bind('typeof gap === "number" ? gap + "rpx" : gap');

        &:last-child {
          margin-right: 0;
        }
      }
    }
  }

  &__content {
    flex-shrink: 0;
    height: 100%;
    display: flex;
    align-items: center;
  }
}
</style>