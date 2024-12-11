# WHT-Tag 优雅标签组件

一个简约而不简单的标签组件，支持多种样式和渐变效果，让您的应用更加精致。

## 平台兼容性

| 平台 | 支持情况 | 自测说明 |
| --- | --- | --- |
| H5 | ✓ | 已测试主流浏览器，完美适配 |
| 微信小程序 | ✓ | 已测试，功能正常 |
| App-vue | ✓ | 已测试，功能正常 |
| App-nvue | × | 暂不支持 |
| 支付宝小程序 | - | 理论支持，需自测 |
| 百度小程序 | - | 理论支持，需自测 |
| 字节小程序 | - | 理论支持，需自测 |
| QQ小程序 | - | 理论支持，需自测 |
| 其他平台 | - | 理论支持，需自测 |

> 注：
> 1. ✓ 表示已测试，功能正常
> 2. × 表示不支持
> 3. - 表示理论支持，需要自行测试
> 4. 如在其他平台使用遇到问题，欢迎反馈

## 安装方式

通过 uni_modules 在插件市场导入即可。

## 基本用法

```vue
<template>
  <wht-tag>默认标签</wht-tag>
  <wht-tag type="primary">主要标签</wht-tag>
  <wht-tag type="success">成功标签</wht-tag>
  <wht-tag type="warning">警告标签</wht-tag>
  <wht-tag type="error">错误标签</wht-tag>
</template>
```

## 渐变标签

```vue
<template>
  <wht-tag gradient="linear-gradient(45deg, #12c2e9, #c471ed)" round>
    渐变标签
  </wht-tag>
</template>
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| type | 标签类型，可选值：default/primary/success/warning/error/info | String | default |
| color | 自定义标签颜色 | String | - |
| gradient | 渐变背景，如：linear-gradient(45deg, #12c2e9, #c471ed) | String | - |
| text-color | 文字颜色 | String | - |
| size | 标签尺寸，可选值：default/mini | String | default |
| plain | 是否空心 | Boolean | false |
| round | 是否圆角 | Boolean | false |
| mark | 是否标记样式 | Boolean | false |
| closeable | 是否可关闭 | Boolean | false |
| disabled | 是否禁用 | Boolean | false |

### Events

| 事件名 | 说明 | 回调参数 |
| --- | --- | --- |
| click | 点击标签时触发 | event: Event |
| close | 关闭标签时触发 | event: Event |

## 注意事项

1. 渐变效果在不同平台可能有细微差异
2. App-nvue 暂不支持渐变效果
3. 建议在使用前在目标平台进行测试