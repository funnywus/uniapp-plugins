# wht-select 选择器组件

## 介绍
一个简单易用的下拉选择器组件，支持丰富的样式定制。

## 使用方法

```vue
<template>
	<wht-select v-model="value" :options="options" placeholder="请选择" />
</template>
<script>
export default {
	data() {
		return {
			value: '',
			options: [
				{ label: '选项一', value: '1' },
				{ label: '选项二', value: '2' },
				{ label: '选项三', value: '3' }
			]
		}
	}
}
</script>
```

## Props 属性说明

| 参数 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| value/v-model | 绑定值 | string/number | - |
| options | 选项数据 | array | [] |
| placeholder | 占位符 | string | '请选择' |
| disabled | 是否禁用 | boolean | false |
| clearable | 是否可清除 | boolean | false |
| height | 选择器高度 | number | 40 |
| fontSize | 字体大小 | number | 14 |
| borderColor | 边框颜色 | string | '#dcdfe6' |
| borderRadius | 圆角大小 | number | 4 |
| backgroundColor | 背景颜色 | string | '#ffffff' |
| textColor | 文字颜色 | string | '#606266' |
| placeholderColor | 占位符颜色 | string | '#c0c4cc' |
| activeColor | 激活状态颜色 | string | '#409eff' |
| filterable | 是否开启搜索功能 | Boolean | false |

## Events 事件说明

| 事件名 | 说明 | 回调参数 |
|--------|------|----------|
| change | 选中值发生变化时触发 | 目前选中的值 |
| clear | 点击清除按钮时触发 | - |
| search | 搜索输入时触发 | (query: string) 搜索关键词 |

### Options 数据结构

```js
{
  label: string,  // 显示的文本
  value: string/number,  // 选项的值
  disabled?: boolean  // 是否禁用该选项
}
```

## 代码示例

### 基础用法

```vue
<template>
	<wht-select v-model="value" :options="options" placeholder="请选择" />
</template>
<script>
export default {
	data() {
		return {
			value: '',
			options: [
				{ label: '选项一', value: '1' },
				{ label: '选项二', value: '2' },
				{ label: '选项三', value: '3' }
			]
		}
	}
}
</script>
```

### 可搜索

```vue
<template>
	<wht-select v-model="value" :options="options" placeholder="请选择" filterable />
</template>
<script>
export default {
	data() {
		return {
			value: '',
			options: [
				{ label: '选项一', value: '1' },
				{ label: '选项二', value: '2' },
				{ label: '选项三', value: '3' }
			]
		}
	}
}
</script>
```
