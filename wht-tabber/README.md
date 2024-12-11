# wht-tabbar 底部导航栏组件

一个基于 uni-app 开发的跨平台底部导航栏组件，支持自定义样式和丰富的配置选项。

## 特性

- 📱 支持所有主流平台
- 🎨 支持自定义图标和样式
- 🔥 支持徽标显示和动画效果
- ⚡️ 支持凸起按钮样式
- 💫 平滑切换动画

## 安装

在 uni-app 项目中，从插件市场导入该组件即可使用。

## 基础用法

```vue
<template>
  <wht-tabbar v-model="current" :list="tabList">
    <view class="content">
      页面内容区域
    </view>
  </wht-tabbar>
</template>

<script>
export default {
  data() {
    return {
      current: 0,
      tabList: [
        {
          text: '首页',
          icon: '/static/tabbar/home.png',
          selectedIcon: '/static/tabbar/home-active.png'
        },
        {
          text: '分类',
          icon: '/static/tabbar/cate.png',
          selectedIcon: '/static/tabbar/cate-active.png'
        },
        {
          text: '我的',
          icon: '/static/tabbar/user.png',
          selectedIcon: '/static/tabbar/user-active.png'
        }
      ]
    }
  }
}
</script>
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| list | 底部导航数据 | Array | [] |
| current | 当前选中项 | Number | 0 |
| color | 文字默认颜色 | String | #999999 |
| selectedColor | 文字选中颜色 | String | #000000 |
| backgroundColor | 背景颜色 | String | #ffffff |
| borderStyle | 上边框样式 | String | black |
| height | 高度 | Number | 50 |
| bulge | 是否开启凸起按钮 | Boolean | false |
| bulgeIndex | 凸起按钮索引 | Number | -1 |

### Events

| 事件名 | 说明 | 回调参数 |
|--------|------|----------|
| change | 切换标签时触发 | index: 当前选中项的索引 |

### TabItem 数据结构

```typescript
interface TabItem {
  text: string;           // 标签文字
  icon: string;           // 未选中图标
  selectedIcon: string;   // 选中图标
  badge?: number|string;  // 徽标内容
  dot?: boolean;         // 是否显示小红点
}
```

## 示例场景

### 1. 基础导航栏
最基本的底部导航功能

### 2. 带徽标导航栏
支持显示消息提醒和小红点

### 3. 凸起按钮
支持中间凸起的特殊按钮样式

### 4. 自定义样式
可自定义图标、颜色和动画效果

## 注意事项

1. 建议图标尺寸保持一致，推荐 40x40
2. 凸起按钮高度会自动调整
3. 徽标超过99将显示为 99+
4. 建议不要超过5个导航项

## 更新日志

### v1.0.0
- 🎉 首次发布
- ✨ 支持基础导航功能
- 🆕 支持徽标显示
- 📦 支持凸起按钮
- 🎨 支持自定义样式

## 贡献指南

欢迎提交 Issue 或 Pull Request 来完善这个组件。

## 许可证

[MIT](LICENSE) © 2024