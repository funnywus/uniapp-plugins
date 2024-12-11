# wht-search 轻量级搜索框组件

一个优雅、轻量、可定制的搜索框组件，支持多端兼容。

## 平台兼容性
* App-vue: 支持
* App-nvue: 支持
* H5: 支持
* 微信小程序: 支持
* 支付宝小程序: 支持
* QQ小程序: 支持

## 安装方式

### 插件依赖
本组件依赖 `uni-icons` 图标组件，请确保项目中已安装该组件：
1. 在插件市场打开[uni-icons](https://ext.dcloud.net.cn/plugin?id=28)，点击安装
2. 或者在HBuilderX中点击菜单【工具】->【插件安装】，搜索 `uni-icons` 安装

### 组件安装
通过uni_modules安装，在插件市场打开，点击安装即可。

## 基础用法

```vue
<template>
    <wht-search v-model="searchText" @search="onSearch" />
</template>
<script>
export default {
    data() {
        return {
            searchText: ''
        }
    },
    methods: {
        onSearch(value) {
            console.log('搜索:', value)
        }
    }
}
</script>
```

## API

### Props 属性
| 属性名 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| v-model | String | '' | 搜索框的值 |
| placeholder | String | '请输入搜索关键词' | 占位提示文字 |
| autoFocus | Boolean | false | 是否自动聚焦 |
| showClear | Boolean | true | 是否显示清除按钮 |
| showSearchBtn | Boolean | true | 是否显示搜索按钮 |
| searchText | String | '搜索' | 搜索按钮文字 |

### Events 事件
| 事件名 | 说明 | 回调参数 |
| --- | --- | --- |
| @search | 点击搜索按钮时触发 | value: 搜索框的值 |
| @clear | 点击清除按钮时触发 | - |
| @focus | 输入框聚焦时触发 | event: Event |
| @blur | 输入框失焦时触发 | event: Event |
| @confirm | 点击完成按钮时触发 | value: 搜索框的值 |

### Slots 插槽
| 名称 | 说明 |
| --- | --- |
| left | 自定义左侧内容 |
| search-btn | 自定义搜索按钮 |

### 样式定制
组件提供了丰富的样式定制属性：

```vue
<template>
  <wht-search
    v-model="searchText"
    :content-style="{ 
      background: '#f0f2f5',
      borderRadius: '100rpx'
    }"
    :search-btn-style="{
      background: '#2979ff',
      borderRadius: '100rpx'
    }"
  />
</template>
```

更多使用示例请参考demo。