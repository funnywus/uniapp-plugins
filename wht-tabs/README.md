# wht-tabs 选项卡组件

一个基于 uni-app 开发的跨平台选项卡组件，支持多种常用场景。

## 特性

- 🚀 轻量级设计，性能优化
- 💪 跨平台兼容，支持多端运行
- 🎨 高度可定制，满足不同场景
- 📦 使用简单，配置灵活

## 安装

在 uni-app 项目中，从插件市场导入该组件即可使用。

## 基础用法

```vue
<template>
  <wht-tabs :tabs="tabs" v-model="current">
    <view class="content">
      当前选中项: {{current}}
    </view>
  </wht-tabs>
</template>

<script>
export default {
  data() {
    return {
      current: 0,
      tabs: ['选项1', '选项2', '选项3']
    }
  }
}
</script>
```

## 功能示例

### 1. 基础用法
最简单的选项卡切换效果

### 2. 吸顶效果
支持页面滚动时选项卡固定在顶部

### 3. 搜索列表
结合搜索功能的选项卡列表

### 4. 商品分类
适用于电商场景的分类切换

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| tabs | 选项卡数据 | Array | [] |
| current | 当前选中项 | Number | 0 |
| sticky | 是否开启吸顶 | Boolean | false |
| stickyTop | 吸顶距离 | Number | 0 |

### Events

| 事件名 | 说明 | 回调参数 |
|--------|------|----------|
| change | 选项卡切换时触发 | index: 当前选中项的索引 |

## 注意事项

1. 组件依赖 uni-app 环境
2. 建议在页面 onLoad 时初始化数据
3. 吸顶效果在不同平台可能存在差异

## 更新日志

### v1.0.0
- 🎉 首次发布
- ✨ 支持基础选项卡功能
- 🆕 添加吸顶效果
- 📦 支持自定义样式

## 贡献指南

欢迎提交 Issue 或 Pull Request 来完善这个组件。

## 许可证

[MIT](LICENSE) © 2024
