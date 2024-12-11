<template>
  <view class="wht-poster">
    <canvas 
      canvas-id="whtPosterCanvas" 
      id="whtPosterCanvas" 
      class="poster-canvas"
      :style="{width: width + 'rpx', height: height + 'rpx'}"
      :width="canvasWidth"
      :height="canvasHeight">
    </canvas>
  </view>
</template>

<script>
export default {
  name: 'wht-canvas-poster',
  props: {
    width: {
      type: Number,
      default: 300
    },
    height: {
      type: Number,
      default: 450
    },
    posterConfig: {
      type: Object,
      default: () => ({})
    }
  },
  data() {
    return {
      ctx: null,
      dpr: 1,
      canvasWidth: 300,
      canvasHeight: 450
    }
  },
  mounted() {
    this.dpr = uni.getSystemInfoSync().pixelRatio || 2
    this.canvasWidth = this.width * this.dpr
    this.canvasHeight = this.height * this.dpr
    this.initCanvas()
  },
  methods: {
    // 初始化画布
    initCanvas() {
      // #ifdef MP || APP-PLUS
      this.ctx = uni.createCanvasContext('whtPosterCanvas', this)
      this.$emit('canvasReady')
      // #endif

      // #ifdef H5
      const query = uni.createSelectorQuery().in(this)
      query.select('#whtPosterCanvas')
        .fields({ node: true, size: true })
        .exec((res) => {
          if (res[0]) {
            const canvas = res[0].node
            this.ctx = canvas.getContext('2d')
            this.ctx.scale(this.dpr, this.dpr)
            this.$emit('canvasReady')
          }
        })
      // #endif
    },

    // 获取图片信息，包括宽高
    async getImageInfo(src) {
      console.log('开始获取图片信息:', src)
      return new Promise((resolve, reject) => {
        uni.getImageInfo({
          src: src,
          success: (res) => {
            console.log('获取图片信息成功:', res)
            resolve({
              path: res.path,
              width: res.width,
              height: res.height
            })
          },
          fail: (err) => {
            console.error('获取图片信息失败:', err)
            reject(err)
          }
        })
      })
    },

    // 计算适配后的尺寸
    calculateSize(originalWidth, originalHeight, maxWidth, maxHeight) {
      let width = originalWidth
      let height = originalHeight
      
      // 如果指定了最大宽度
      if (maxWidth && width > maxWidth) {
        height = (maxWidth / width) * height
        width = maxWidth
      }
      
      // 如果高度仍然超出最大高度
      if (maxHeight && height > maxHeight) {
        width = (maxHeight / height) * width
        height = maxHeight
      }
      
      return {
        width: Math.round(width),
        height: Math.round(height)
      }
    },

    // 绘制图片
    async drawImage(src, x, y, maxWidth, maxHeight) {
      if (!this.checkCanvasReady()) return Promise.reject('画布未就绪')
      
      try {
        console.log('开始绘制图片:', src)
        
        // 获取图片信息
        const imageInfo = await this.getImageInfo(src)
        console.log('图片原始尺寸:', imageInfo)
        
        // 计算适配后的尺寸
        const size = this.calculateSize(
          imageInfo.width, 
          imageInfo.height,
          maxWidth || this.width, // 如果没有指定最大宽度，使用画布宽度
          maxHeight || this.height // 如果没有指定最大高度，使用画布高度
        )
        console.log('适配后的尺寸:', size)
        
        return new Promise((resolve, reject) => {
          // #ifdef H5
          const img = new Image()
          img.crossOrigin = 'anonymous'
          img.onload = () => {
            try {
              this.ctx.drawImage(img, x * this.dpr, y * this.dpr, size.width * this.dpr, size.height * this.dpr)
              resolve()
            } catch (e) {
              reject(e)
            }
          }
          img.onerror = reject
          img.src = imageInfo.path
          // #endif

          // #ifdef MP || APP-PLUS
          try {
            this.ctx.drawImage(imageInfo.path, x * this.dpr, y * this.dpr, size.width * this.dpr, size.height * this.dpr)
            this.ctx.draw(true)
            resolve()
          } catch (e) {
            reject(e)
          }
          // #endif
        })
      } catch (error) {
        console.error('绘制图片失败:', error)
        throw error
      }
    },

    // 检查画布是否就绪
    checkCanvasReady() {
      if (!this.ctx) {
        console.error('画布未准备就绪')
        return false
      }
      return true
    },

    // 清空画布
    clear() {
      if (!this.checkCanvasReady()) return
      this.ctx.clearRect(0, 0, this.width, this.height)
      // #ifdef MP || APP-PLUS
      this.ctx.draw(true)
      // #endif
    },

    // 绘制矩形
    drawRect(x, y, width, height, style = {}) {
      if (!this.checkCanvasReady()) return
      this.ctx.fillStyle = style.fill || '#ffffff'
      this.ctx.fillRect(x, y, width, height)
      // #ifdef MP || APP-PLUS
      this.ctx.draw(true)
      // #endif
    },

    // 绘制文本
    drawText(text, x, y, style = {}) {
      if (!this.checkCanvasReady()) return
      const fontSize = style.size || 28
      const fontWeight = style.bold ? 'bold' : 'normal'
      this.ctx.font = `${fontWeight} ${fontSize * this.dpr}px sans-serif`
      this.ctx.fillStyle = style.color || '#000000'
      this.ctx.textAlign = style.align || 'left'
      this.ctx.fillText(text, x * this.dpr, y * this.dpr)
      // #ifdef MP || APP-PLUS
      this.ctx.draw(true)
      // #endif
    },

    // 处理 margin
    handleMargin(element) {
      const margin = element.margin || {}
      return {
        top: margin.top || margin.y || 0,
        right: margin.right || margin.x || 0,
        bottom: margin.bottom || margin.y || 0,
        left: margin.left || margin.x || 0
      }
    },

    // 开始绘制
    async draw() {
      if (!this.checkCanvasReady()) return
      
      try {
        uni.showLoading({
          title: '生成中...'
        })
        
        this.clear()
        console.log('开始绘制海报')
        
        const config = this.posterConfig
        
        // 绘制背景
        if (config.background) {
          this.drawRect(0, 0, this.width * this.dpr, this.height * this.dpr, { fill: config.background })
        }
        
        // 绘制元素
        if (config.elements) {
          for (let element of config.elements) {
            try {
              const margin = this.handleMargin(element)
              console.log('绘制元素:', element.type, '边距:', margin)
              
              switch (element.type) {
                case 'image':
                  await this.drawImage(
                    element.src,
                    element.x + (margin.left || 0),
                    element.y + (margin.top || 0),
                    element.maxWidth, // 可选的最大宽度
                    element.maxHeight // 可选的最大高度
                  )
                  break
                case 'text':
                  this.drawText(
                    element.text,
                    element.x + (margin.left || 0),
                    element.y + (margin.top || 0),
                    element.style
                  )
                  break
              }
            } catch (elementError) {
              console.error('绘制元素失败:', elementError, element)
            }
          }
        }
        
        // #ifdef MP || APP-PLUS
        this.ctx.draw(true, () => {
          uni.hideLoading()
          this.$emit('drawn')
        })
        // #endif

        // #ifdef H5
        uni.hideLoading()
        this.$emit('drawn')
        // #endif
      } catch (e) {
        uni.hideLoading()
        console.error('绘制失败:', e)
        throw e
      }
    },

    // 保存到相册
    async saveToAlbum() {
      if (!this.checkCanvasReady()) return Promise.reject('画布未就绪')
      
      return new Promise((resolve, reject) => {
        uni.canvasToTempFilePath({
          canvasId: 'whtPosterCanvas',
          success: (res) => {
            uni.saveImageToPhotosAlbum({
              filePath: res.tempFilePath,
              success: () => {
                uni.showToast({
                  title: '保存成功',
                  icon: 'success'
                })
                resolve()
              },
              fail: (err) => {
                console.error('保存失败:', err)
                uni.showToast({
                  title: '保存失败',
                  icon: 'none'
                })
                reject(err)
              }
            })
          },
          fail: reject
        }, this)
      })
    }
  }
}
</script>

<style>
.wht-poster {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}
.poster-canvas {
  background: #ffffff;
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.1);
  border-radius: 8rpx;
}
</style>