# wht-input 增强输入框组件

## 介绍
wht-input 是一个功能强大的输入框组件，支持自定义主题颜色、圆角、图标、插槽等特性，适配多端。

### 平台支持
- App Vue
- H5
- 微信小程序
- 支付宝小程序
- 钉钉小程序
- QQ小程序
- 字节小程序

## 安装方式
下载插件后，导入项目即可使用

## 基本用法

### 基础示例
```vue
<template>
	<view class="content">
		<!-- 基础输入框 -->
		<wht-input v-model="input1" placeholder="默认输入框"></wht-input>
		<!-- 带图标的输入框 -->
		<wht-input v-model="input2" prefix-icon="search" placeholder="搜索框"></wht-input>
		<!-- 自定义主题色 -->
		<wht-input v-model="input3" border-color="#409eff" text-color="#409eff" icon-color="#409eff"
			placeholder="自定义主题色"></wht-input>
		<!-- 带插槽的输入框 -->
		<wht-input v-model="input4" placeholder="带插槽的输入框">
			<template #prefix>￥</template>
			<template #suffix>.00</template>
		</wht-input>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				input1: '',
				input2: '',
				input3: '',
				input4: ''
			}
		}
	}
</script>
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| modelValue/v-model | 绑定值 | String/Number | '' |
| type | 输入框类型 | String | 'text' |
| placeholder | 占位文本 | String | '请输入' |
| disabled | 是否禁用 | Boolean | false |
| clearable | 是否可清空 | Boolean | false |
| maxlength | 最大输入长度 | Number | -1 |
| prefixIcon | 前置图标 | String | '' |
| suffixIcon | 后置图标 | String | '' |
| password | 是否密码框 | Boolean | false |
| focus | 是否自动获取焦点 | Boolean | false |
| borderColor | 边框颜色 | String | '#dcdfe6' |
| backgroundColor | 背景颜色 | String | '#ffffff' |
| textColor | 文字颜色 | String | '#606266' |
| iconColor | 图标颜色 | String | '#999' |
| placeholderColor | 占位文本颜色 | String | '#c0c4cc' |
| radius | 圆角大小 | Number/String | 4 |

### Events

| 事件名 | 说明 | 回调参数 |
| --- | --- | --- |
| input | 输入时触发 | (event: Event) |
| focus | 获得焦点时触发 | (event: Event) |
| blur | 失去焦点时触发 | (event: Event) |
| confirm | 点击完成按钮时触发 | (event: Event) |
| clear | 点击清除按钮时触发 | - |

### Slots

| 名称 | 说明 |
| --- | --- |
| prefix | 输入框前置内容 |
| suffix | 输入框后置内容 |

## 注意事项
1. 组件依赖 uni-icons，请确保项目中已安装该组件
2. 在 nvue 页面中可能存在部分样式不生效的情况
3. 部分平台可能不支持某些特定的 type 类型