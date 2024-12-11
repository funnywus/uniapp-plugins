<template>
  <view 
    class="wht-link"
    :class="classes"
    :style="styles"
    @click="onClick"
  >
    <slot name="prefix"></slot>
    <slot>{{ text }}</slot>
    <slot name="suffix"></slot>
  </view>
</template>

<script>
const LINK_TYPES = ['primary', 'success', 'warning', 'danger', 'info']

// #ifdef VUE3
import { computed } from 'vue'

export default {
  name: 'wht-link',
  props: {
    type: {
      type: String,
      default: 'primary',
      validator: value => LINK_TYPES.includes(value)
    },
    text: {
      type: String,
      default: ''
    },
    href: {
      type: String,
      default: ''
    },
    underline: {
      type: Boolean,
      default: true
    },
    disabled: {
      type: Boolean,
      default: false
    },
    download: {
      type: Boolean,
      default: false
    },
    filename: {
      type: String,
      default: ''
    },
    customStyle: {
      type: Object,
      default: () => ({})
    }
  },
  setup(props, { emit }) {
    const classes = computed(() => ([
      `wht-link--${props.type}`,
      { 
        'wht-link--disabled': props.disabled,
        'wht-link--underline': props.underline 
      }
    ]))

    const styles = computed(() => props.customStyle || {})

    const handleDownload = async () => {
      try {
        const response = await fetch(props.href)
        const blob = await response.blob()
        const url = window.URL.createObjectURL(blob)
        const link = document.createElement('a')
        link.style.display = 'none'
        link.href = url
        link.download = props.filename || props.href.split('/').pop() || 'download'
        document.body.appendChild(link)
        link.click()
        document.body.removeChild(link)
        window.URL.revokeObjectURL(url)
      } catch (error) {
        console.error('Download failed:', error)
        uni.showToast({ title: '下载失败', icon: 'none' })
      }
    }

    const onClick = async (e) => {
      if (props.disabled) return
      if (props.href) {
        // #ifdef MP
        uni.setClipboardData({
          data: props.href,
          success: () => uni.showToast({ title: '链接已复制', icon: 'none' })
        })
        // #endif

        // #ifdef H5
        props.download ? await handleDownload() : window.open(props.href, '_blank')
        // #endif
        
        // #ifdef APP-PLUS
        plus.runtime.openURL(props.href)
        // #endif
      }
      emit('click', e)
    }

    return { classes, styles, onClick }
  }
}
// #endif

// #ifdef VUE2
export default {
  name: 'wht-link',
  props: {
    type: {
      type: String,
      default: 'primary',
      validator: value => LINK_TYPES.includes(value)
    },
    text: {
      type: String,
      default: ''
    },
    href: {
      type: String,
      default: ''
    },
    underline: {
      type: Boolean,
      default: true
    },
    disabled: {
      type: Boolean,
      default: false
    },
    download: {
      type: Boolean,
      default: false
    },
    filename: {
      type: String,
      default: ''
    },
    customStyle: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    classes() {
      return [
        `wht-link--${this.type}`,
        { 
          'wht-link--disabled': this.disabled,
          'wht-link--underline': this.underline 
        }
      ]
    },
    styles() {
      return this.customStyle || {}
    }
  },
  methods: {
    async handleDownload() {
      try {
        const response = await fetch(this.href)
        const blob = await response.blob()
        const url = window.URL.createObjectURL(blob)
        const link = document.createElement('a')
        link.style.display = 'none'
        link.href = url
        link.download = this.filename || this.href.split('/').pop() || 'download'
        document.body.appendChild(link)
        link.click()
        document.body.removeChild(link)
        window.URL.revokeObjectURL(url)
      } catch (error) {
        console.error('Download failed:', error)
        uni.showToast({ title: '下载失败', icon: 'none' })
      }
    },
    async onClick(e) {
      if (this.disabled) return
      if (this.href) {
        // #ifdef MP
        uni.setClipboardData({
          data: this.href,
          success: () => uni.showToast({ title: '链接已复制', icon: 'none' })
        })
        // #endif

        // #ifdef H5
        this.download ? await this.handleDownload() : window.open(this.href, '_blank')
        // #endif
        
        // #ifdef APP-PLUS
        plus.runtime.openURL(this.href)
        // #endif
      }
      this.$emit('click', e)
    }
  }
}
// #endif
</script>

<style lang="scss" scoped>
$colors: (
  primary: #409eff,
  success: #67c23a,
  warning: #e6a23c,
  danger: #f56c6c,
  info: #909399,
  disabled: #c0c4cc
);

.wht-link {
  display: inline-flex;
  align-items: center;
  font-size: 28rpx;
  font-weight: 500;
  text-decoration: none;
  cursor: pointer;

  @each $type, $color in $colors {
    &--#{$type} {
      color: $color;
    }
  }

  &--disabled {
    cursor: not-allowed;
  }

  &--underline {
    &:not(.wht-link--disabled):hover {
      text-decoration: underline;
    }
  }
}
</style>
