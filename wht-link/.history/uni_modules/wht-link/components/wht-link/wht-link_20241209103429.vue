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

<script setup>
import { computed } from 'vue'

const LINK_TYPES = ['primary', 'success', 'warning', 'danger', 'info']

defineOptions({
  name: 'wht-link'
})

const props = defineProps({
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
})

const emit = defineEmits(['click'])

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
