# wht-radio 单选框组件

一个功能强大、易用的单选框组件，支持普通模式和列表模式，可自定义主题颜色。

## 平台兼容性
* H5 - 支持
* 小程序 - 支持
* App - 支持
* Vue2 - 支持
* Vue3 - 支持

## 基本用法
```vue
<template>
    <wht-radio v-model="value" :options="options" @change="onChange" />
</template>
<script>
export default {
    data() {
        return {
            value: '1',
            options: [
                { label: '选项1', value: '1' },
                { label: '选项2', value: '2' },
                { label: '选项3', value: '3' }
            ]
        }
    },
    methods: {
        onChange(value) {
            console.log('选中值：', value)
        }
    }
}
</script>
```


## 组件属性

| 属性名 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| modelValue/v-model | String/Number | '' | 选中项的值 |
| options | Array | [] | 选项数组，格式：[{label: '显示文本', value: '值'}] |
| type | String | 'normal' | 显示类型，可选值：'normal'(普通模式)/'list'(列表模式) |
| disabled | Boolean | false | 是否禁用 |
| color | String | '#007AFF' | 选中状态的主题颜色 |

## 组件事件

| 事件名 | 说明 | 回调参数 |
| --- | --- | --- |
| change | 选中值发生变化时触发 | value: 当前选中的值 |

## 示例展示

### 普通模式
```vue
<wht-radio v-model="value" :options="options" />
```

### 列表模式
```vue
<wht-radio v-model="value" type="list" :options="options" />
```

### 自定义颜色
```vue
<wht-radio v-model="value" :options="options" color="#FF0000" />
```

### 禁用状态
```vue
<wht-radio v-model="value" :options="options" disabled />
```