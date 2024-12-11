# wht-link 链接组件

一个优雅的链接组件，支持多平台（H5、小程序、App）和多框架（Vue2、Vue3）。

## 特性 ✨

- 🎨 多种主题样式（primary、success、warning、danger、info）
- 🔗 智能的平台适配（H5直接跳转、小程序复制链接、App打开系统浏览器）
- 📦 支持 H5 文件下载
- 🎯 完整的 TypeScript 类型支持
- 💫 丰富的自定义选项
- ⚡️ 支持 Vue2/Vue3 双版本

## 平台兼容性 🔌

| 平台       | 支持情况 |
|-----------|---------|
| H5        | ✅      |
| 微信小程序  | ✅      |
| App       | ✅      |
| 其他平台    | 自测     |

### 框架支持

| 框架版本    | 支持情况 | 备注 |
|-----------|---------|------|
| Vue 2     | ✅      | 使用 Options API |
| Vue 3     | ✅      | 使用 Composition API |

## 安装 📦

在 uni-app 插件市场中搜索并导入 `wht-link`，或者直接导入本地插件。

## 基础用法 🚀

### Vue 3 示例

```vue
<template>
  <wht-link text="默认链接"></wht-link>
  <wht-link type="primary" text="主要链接"></wht-link>
  <wht-link type="success" text="成功链接"></wht-link>
  <wht-link type="warning" text="警告链接"></wht-link>
  <wht-link type="danger" text="危险链接"></wht-link>
  <wht-link type="info" text="信息链接"></wht-link>
</template>
```

### Vue 2 示例

```vue
<template>
  <wht-link text="默认链接"></wht-link>
  <wht-link type="primary" text="主要链接"></wht-link>
  <wht-link type="success" text="成功链接"></wht-link>
  <wht-link type="warning" text="警告链接"></wht-link>
  <wht-link type="danger" text="危险链接"></wht-link>
  <wht-link type="info" text="信息链接"></wht-link>
</template>
```

## API 📚

### Props

| 参数 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| type | 链接类型，可选值：primary / success / warning / danger / info | string | primary |
| text | 链接文本 | string | - |
| href | 链接地址 | string | - |
| underline | 是否显示下划线 | boolean | true |
| disabled | 是否禁用 | boolean | false |
| download | 是否为下载链接（仅H5平台支持） | boolean | false |
| filename | 下载文件名（仅H5平台且download为true时生效） | string | - |
| customStyle | 自定义样式 | object | {} |

### Events

| 事件名 | 说明 | 回调参数 |
|-------|------|---------|
| click | 点击链接时触发 | event: Event |

### Slots

| 插槽名 | 说明 |
|--------|------|
| default | 默认插槽，链接内容 |
| prefix | 前缀图标 |
| suffix | 后缀图标 |

## 平台差异说明 🌐

1. H5 平台
   - 支持直接链接跳转
   - 支持文件下载功能
   - 支持新窗口打开

2. 小程序平台
   - 自动复制链接到剪贴板
   - 显示复制成功提示

3. App 平台
   - 使用系统浏览器打开链接

## 最佳实践 💡

1. 链接类型选择
   - 使用 `primary` 作为主要操作
   - 使用 `success` 表示成功或正向操作
   - 使用 `warning` 表示需要注意的操作
   - 使用 `danger` 表示危险或不可逆操作
   - 使用 `info` 表示普通信息

2. 文件下载（H5）
   ```vue
   <wht-link
     href="https://example.com/file.pdf"
     download
     filename="自定义文件名.pdf"
   >
     下载文件
   </wht-link>
   ```

3. 自定义样式
   ```vue
   <wht-link :customStyle="{ fontSize: '32rpx', fontWeight: 'bold' }">
     自定义样式
   </wht-link>
   ```

4. 使用插槽
   ```vue
   <wht-link>
     <template #prefix>
       <text class="icon">🔗</text>
     </template>
     链接文本
     <template #suffix>
       <text class="icon">→</text>
     </template>
   </wht-link>
   ```

## 注意事项 ⚠️

1. 下载功能仅在 H5 平台可用
2. 需要确保链接地址的安全性和可访问性
3. 在小程序中会自动处理为复制链接功能
4. App 端会调用系统浏览器打开链接

## 贡献 🤝

欢迎提交 issue 和 PR，一起完善这个组件！