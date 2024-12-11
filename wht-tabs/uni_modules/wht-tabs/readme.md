# wht-tabs 标签组件

## 介绍
一个简单易用的标签组件，支持自定义样式等功能。

## 平台支持
- Vue2/Vue3
- H5/APP/小程序

## 基础用法

```vue
<template>
  <wht-tabs 
    v-model="active" 
    :list="tabList"
    @change="onChange"
  />
</template>

<script>
export default {
  data() {
    return {
      active: 0,
      tabList: [
        { title: '标签1' },
        { title: '标签2' },
        { title: '标签3' }
      ]
    }
  },
  methods: {
    onChange(index) {
      console.log('当前选中:', index)
    }
  }
}
</script>
```

## 吸顶用法

```vue
<template>
  <wht-tabs 
    v-model="active" 
    :list="tabList"
    :fixed="true"
    :top="0"
    @change="onChange"
  />
</template>
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| list | 标签数据列表 | Array | [] |
| modelValue(v-model) | 当前选中标签的索引 | Number | 0 |
| fixed | 是否固定在顶部 | Boolean | false |
| top | 固定在顶部时的距离(px) | Number | 0 |
| activeColor | 选中状态的颜色 | String | #2979ff |
| color | 默认状态的颜色 | String | #666666 |
| bgColor | 背景颜色 | String | #ffffff |
| fontSize | 字体大小(rpx) | Number | 28 |
| height | 选项卡高度(rpx) | Number | 88 |
| padding | 选项左右内边距(rpx) | Number | 30 |
| lineHeight | 底部线条高度(rpx) | Number | 4 |
| bold | 是否加粗选中项 | Boolean | true |
| minWidth | 选项最小宽度(rpx) | Number | 120 |

### Events

| 事件名 | 说明 | 回调参数 |
| --- | --- | --- |
| change | 切换标签时触发 | index: number |

### list 数据结构

```js
list: [
  { 
    title: '标签标题'  // 标签文字
  }
]
```

## 示例

### 自定义样式

```vue
<template>
  <wht-tabs 
    v-model="active" 
    :list="tabList"
    activeColor="#ff4444"
    color="#999999"
    :fontSize="32"
    :height="100"
    :padding="40"
    :lineHeight="6"
    bgColor="#f8f8f8"
    :bold="true"
    :minWidth="160"
    @change="onChange"
  />
</template>
```

## 更新日志

### 1.0.0（2024-01-01）
- 首次发布
- 支持基础标签切换功能
- 支持自定义样式
- 支持Vue2/Vue3
- 支持H5/APP/小程序