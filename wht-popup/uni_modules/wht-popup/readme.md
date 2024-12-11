# WHT-Popup 弹出层组件
一个优雅的弹出层组件，支持多个方向弹出，可自定义内容。轻量、灵活、易用。

## 介绍
- 支持多个方向弹出：上、下、左、右、中间
- 支持自定义内容和样式
- 支持遮罩层点击关闭
- 支持关闭按钮显示/隐藏
- 平滑的动画过渡效果

## 平台兼容性
| H5  | App | 微信小程序 | 支付宝小程序 | 抖音小程序 |
| --- | --- | ---------- | ------------ | ---------- |
| √   | √   | √          | √            | √          |

## 基础用法

```vue
<template>
    <wht-popup v-model:show="show" position="center">
        <view>弹窗内容</view>
    </wht-popup>
</template>
<script>
export default {
    data() {
        return {
            show: false
        }
    }
}
</script>
```

## API

### Props
| 参数         | 说明         | 类型    | 默认值  |
|--------------|-------------|---------|---------|
| show         | 是否显示弹窗 | Boolean | false   |
| position     | 弹出位置     | String  | center  |
| clearable    | 显示关闭按钮 | Boolean | true   |
| maskClosable | 点击遮罩关闭 | Boolean | true    |

### Events
| 事件名  | 说明     | 回调参数 |
|---------|---------|----------|
| open    | 打开弹窗 | -        |
| close   | 关闭弹窗 | -        |

### position 可选值
| 值     | 说明   |
|--------|--------|
| center | 居中   |
| top    | 顶部   |
| bottom | 底部   |
| left   | 左侧   |
| right  | 右侧   |