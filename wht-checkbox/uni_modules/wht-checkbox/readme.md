# wht-checkbox

一个增强版的复选框组件，支持自定义样式、列表模式等功能。

## 平台兼容性
- H5
- 微信小程序
- APP
- 其他平台未测试

## 安装方式
下载插件后，在 `uni_modules` 目录下导入。

## 基础用法
```vue
<template>
    <!-- 基础用法 -->
    <wht-checkbox v-model="checked">选项1</wht-checkbox>
    <!-- 自定义颜色 -->
    <wht-checkbox v-model="checked" activeColor="#07c160">绿色主题</wht-checkbox>
    <!-- 列表模式 -->
    <wht-checkbox v-model="checkedList" :options="options" isList @change="onChange" />
</template>
<script>
export default {
    data() {
        return {
            checked: false,
            checkedList: ['1'],
            options: [
                { label: '选项1', value: '1' },
                { label: '选项2', value: '2' },
                { label: '选项3', value: '3' }
            ]
        }
    }
}
</script>
```

## API

### Props 属性说明
| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| modelValue/v-model | 绑定值 | Boolean/Array | false |
| activeColor | 选中状态的颜色 | String | #1989fa |
| disabled | 是否禁用 | Boolean | false |
| shape | 形状，可选值：square/round | String | square |
| isList | 是否为列表模式 | Boolean | false |
| inline | 是否行内布局（列表模式有效） | Boolean | false |
| options | 列表选项数据（列表模式必填） | Array | - |

### options 数据结构
```js
[
    {
        label: '选项文字', // 显示的文字
        value: '选项值', // 选项的值
        disabled: false // 是否禁用
    }
]
```

### Events 事件说明
| 事件名 | 说明 | 回调参数 |
| --- | --- | --- |
| change | 值变化时触发 | value: Boolean/Array |

## 示例展示
1. 基础用法
2. 自定义颜色
3. 形状展示（方形/圆形）
4. 禁用状态
5. 列表模式
6. 行内布局

## 更新日志
### 1.0.0
- 基础功能实现
- 支持自定义颜色
- 支持列表模式
- 支持行内布局
- 支持暗黑模式

## 注意事项
1. 列表模式必须传入 options 数组
2. v-model 在非列表模式下为 Boolean 类型，列表模式下为 Array 类型

## 作者
wht

## 开源协议
MIT