# wht-img-upload

一个简单易用的图片上传组件，支持单图/多图上传，适用于 uni-app 项目。

## 特性
- 支持单图/多图上传
- 支持自定义列数和间距
- 支持上传进度显示
- 支持预览和删除
- 支持自定义上传配置

## 安装

在插件市场中搜索 `wht-img-upload` 并导入到项目中。

## 基础用法

```vue
<template>
    <wht-img-upload v-model="imageList" />
</template>
<script>
export default {
    data() {
        return {
            imageList: []
        }
    }
}
</script>
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| modelValue/v-model | 图片列表 | Array | [] |
| max | 最大上传数量 | Number | 9 |
| mode | 上传模式，可选值：single/multi | String | 'multi' |
| columns | 列数 | Number | 3 |
| gap | 间距(rpx) | Number | 24 |
| itemHeight | 图片高度(rpx) | Number | 216 |
| buttonText | 上传按钮文字 | String | '上传图片' |
| showButtonText | 是否显示按钮文字 | Boolean | true |
| uploadConfig | 上传配置 | Object | - |

### Events

| 事件名 | 说明 | 回调参数 |
|------|------|------|
| update:modelValue | 图片列表更新时触发 | imageList |
| choose | 选择图片后触发 | imageList |
| delete | 删除图片时触发 | index |
| error | 上传错误时触发 | error |
