# wht-rate 评分组件

一个功能丰富、易用的评分组件，支持自定义样式、半星评分等特性。

## 平台兼容性

| H5  | 微信小程序 | APP-VUE | APP-NVUE |
|-----|------------|---------|-----------|
| ✓   | ✓         | ✓       | ✓         |

## 基础用法

```vue
<template>
  <wht-rate v-model="value" />
</template>

<script>
export default {
  data() {
    return {
      value: 3
    }
  }
}
</script>
```

## 组件属性

### Props

| 属性名 | 说明 | 类型 | 默认值 |
|--------|------|------|--------|
| v-model | 当前评分值 | Number | 0 |
| max | 最大评分值 | Number | 5 |
| size | 图标大小(rpx) | Number | 40 |
| icon | 选中时的图标 | String | ★ |
| voidIcon | 未选中时的图标 | String | ☆ |
| activeColor | 选中时的颜色 | String | #FFB800 |
| voidColor | 未选中时的颜色 | String | #C8C9CC |
| disabled | 是否禁用 | Boolean | false |
| allowHalf | 是否允许半星 | Boolean | false |
| readonly | 是否只读 | Boolean | false |
| spacing | 图标间距(rpx) | Number | 4 |

### Events

| 事件名 | 说明 | 回调参数 |
|--------|------|----------|
| change | 评分改变时触发 | value: 当前分值 |
| update:modelValue | 更新v-model的值 | value: 当前分值 |

## 代码示例

### 基础用法
```vue
<wht-rate v-model="value" />
```

### 自定义图标
```vue
<wht-rate 
  v-model="value"
  icon="heart"
  void-icon="heart-o"
  active-color="#FF6666"
/>
```

### 自定义样式
```vue
<wht-rate 
  v-model="value"
  :size="50"
  active-color="#FF0000"
  void-color="#999999"
/>
```

### 半星评分
```vue
<wht-rate 
  v-model="value"
  :allow-half="true"
/>
```

### 禁用状态
```vue
<wht-rate 
  v-model="value"
  disabled
/>
```

### 评价场景示例
```vue
<template>
  <view class="rate-box">
    <view class="rate-item">
      <text class="label">商品评分</text>
      <wht-rate v-model="goodsRate" />
    </view>
    <view class="rate-item">
      <text class="label">服务评分</text>
      <wht-rate v-model="serviceRate" />
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      goodsRate: 5,
      serviceRate: 4
    }
  }
}
</script>
```

## 注意事项

1. 组件依赖 uni-app 环境
2. icon 属性支持任意字符或图标字体
3. 建议评分图标大小保持一致
4. 半星模式下不支持自定义图标

## 常见问题

### Q1: 如何修改图标大小？
使用 size 属性设置，单位为 rpx
```vue
<wht-rate :size="60" />
```

### Q2: 如何使用自定义图标？
可以使用图标字体或 Unicode 字符
```vue
<wht-rate icon="heart" void-icon="heart-o" />
```

### Q3: 如何实现评分说明文字？
可以通过数组映射实现
```vue
<template>
  <view class="rate-wrap">
    <wht-rate v-model="value" />
    <text>{{ rateTexts[value-1] }}</text>
  </view>
</template>

<script>
export default {
  data() {
    return {
      value: 3,
      rateTexts: ['差评', '一般', '满意', '很好', '非常好']
    }
  }
}
</script>
```

## 更新日志

### v1.0.0 (2024-03-20)
- 首次发布
- 基础评分功能
- 支持自定义样式
- 支持半星评分

## 贡献

如果您发现任何问题或有改进建议，欢迎提交 Issue 或 PR。

## 许可证

[MIT](LICENSE) © 2024