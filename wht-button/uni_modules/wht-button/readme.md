# wht-button 按钮组件

## 介绍
一个优雅的按钮组件，支持多种样式配置，适用于 H5、小程序、APP 等多端。

## 平台兼容性
* H5 - 支持
* 微信小程序 - 支持
* 支付宝小程序 - 支持
* APP - 支持

## 安装方式
在插件市场导入插件即可使用，支持 vue2/vue3。

## 基本用法
```vue
<template>
    <!-- 基础按钮 -->
    <wht-button>默认按钮</wht-button>
    <wht-button type="primary">主要按钮</wht-button>
    <!-- 不同类型 -->
    <wht-button type="success">成功按钮</wht-button>
    <wht-button type="warning">警告按钮</wht-button>
    <wht-button type="danger">危险按钮</wht-button>
    <!-- 朴素按钮 -->
    <wht-button plain>朴素按钮</wht-button>
    <!-- 禁用状态 -->
    <wht-button disabled>禁用按钮</wht-button>
    <!-- 加载状态 -->
    <wht-button loading>加载中</wht-button>
    <!-- 不同尺寸 -->
    <wht-button size="large">大号按钮</wht-button>
    <wht-button size="mini">小型按钮</wht-button>
</template>

```

## API

### Props

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|------|------|--------|--------|
| type | 类型 | String | default/primary/success/warning/danger | default |
| size | 尺寸 | String | mini/small/normal/large | normal |
| plain | 是否朴素按钮 | Boolean | - | false |
| round | 是否圆角按钮 | Boolean | - | false |
| disabled | 是否禁用 | Boolean | - | false |
| loading | 是否加载中 | Boolean | - | false |

### Events

| 事件名 | 说明 | 回调参数 |
|--------|------|----------|
| @click | 点击按钮时触发 | event: Event |

## 常见问题
Q: 按钮文字太长显示不全怎么办？
A: 建议按钮文字保持在2-4个字，过长的文字建议使用大号按钮。
