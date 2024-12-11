# 老虎机抽奖组件

一个简单易用、动画流畅的老虎机抽奖组件，适用于营销活动、游戏抽奖等场景，支持自定义奖品和样式。

## 介绍
- 流畅的老虎机动画效果
- 支持自定义列数和内容
- 可自定义动画时长和速度
- 支持预设中奖结果

## 平台兼容性

| App-vue | App-nvue | H5  | 微信小程序 | 支付宝小程序 | 钉钉小程序 |
|---------|----------|-----|------------|--------------|------------|
| √       | x        | √   | √          | √            | √          |

## 使用方式

### 基础用法

```vue
<template>
  <wht-lottery ref="lottery" @finish="onLotteryFinish" />
</template>
<script>
export default {
    methods: {
        // 开始抽奖
        startLottery() {
            this.$refs.lottery.start('1A红♠')
        },
        // 抽奖结束回调
        onLotteryFinish(result) {
            console.log('抽奖结束', result)
        }
    }
}
</script>

### 自定义用法

```vue
<template>
  <wht-lottery 
    ref="lottery"
    :columns="3"
    :column-values="customValues"
    @finish="onLotteryFinish"
  />
</template>

<script>
export default {
  data() {
    return {
      customValues: [
        ['金', '银', '铜'],
        ['特', '一', '二'],
        ['奖', '奖', '奖']
      ]
    }
  }
}
</script>
```

## API

### Props 属性说明
| 属性名       | 类型    | 默认值 | 说明         |
|-------------|---------|--------|-------------|
| columns     | Number  | 4      | 转轮列数     |
| columnValues| Array   | -      | 每列可选值    |
| columnDelay | Number  | 0.15   | 列延迟时间(秒)|
| duration    | Number  | 3.5    | 动画时长(秒)  |
| itemHeight  | Number  | 120    | 格子高度     |

### Events 事件说明
| 事件名  | 说明     | 回调参数 |
|--------|----------|----------|
| finish | 抽奖结束 | result: string |

### Methods 方法说明
| 方法名 | 说明     | 参数 |
|-------|----------|------|
| start | 开始抽奖 | result: string (可选，指定中奖结果) |

## 注意事项
1. App-nvue 暂不支持
2. 建议控制抽奖动画时长在3-6秒之间
3. 自定义奖品时需确保每列数据长度一致