# 跑马灯 RaceLamp

一个简单易用、功能强大的跑马灯组件，支持水平和垂直方向的文字滚动效果。

## 平台兼容性
| H5 | 微信小程序 | App |
|:--:|:--:|:--:|
| √ | √ | √ |

其他平台自测

## 基础用法

```vue
<template>
    <wht-race-lamp>
        <text>欢迎使用跑马灯组件！这是一条基础的跑马灯文字效果。</text>
    </wht-race-lamp>
</template>
```

## API

### Props

| 属性 | 类型 | 默认值 | 说明 |
|:--|:--|:--|:--|
| direction | String | 'left' | 滚动方向，可选值：left/right/up/down |
| speed | Number | 60 | 滚动速度 |
| delay | Number | 0 | 开始滚动的延迟时间（秒） |
| height | String/Number | 80 | 容器高度 |
| autoplay | Boolean | true | 是否自动播放 |

### Slots

| 名称 | 说明 |
|:--|:--|
| default | 滚动内容 |

## 示例项目
[在线演示](https://ext.dcloud.net.cn/plugin?name=wht-race-lamp)
