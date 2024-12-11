# wht-datetime-picker

功能丰富的移动端日期时间选择器，支持多种选择模式和灵活配置。

## 特性

- 支持多种选择模式：日期时间、日期、时间、年份、年月等
- 支持区间选择：日期区间、时间区间
- 支持快捷选项，可自定义和自动确认
- 灵活的日期格式化
- 完善的错误处理和验证
- 优雅的界面和交互

## 兼容性

### 框架支持

- Vue 2
- Vue 3
- UniApp

### 终端支持

| 平台 | 支持度 | 说明 |
| --- | --- | --- |
| H5 | | 支持主流移动端浏览器 |
| 微信小程序 | | 完整支持 |
| App Vue | | 支持 Vue 页面 |

### 浏览器支持

| 浏览器 | 支持度 |
| --- | --- |
| Chrome | |
| Safari | |
| Firefox | |
| Edge | |
| Android Browser | |
| 微信浏览器 | |
| QQ浏览器 | |

## 安装

在插件市场中搜索并导入 `wht-datetime-picker`，或者直接导入项目下的 `uni_modules`。

## 基础用法

```vue
<template>
  <view>
    <!-- 基础选择 -->
    <view class="demo-item" @click="showDatePicker">
      <text>选择日期时间</text>
      <text>{{ dateValue || '请选择' }}</text>
    </view>

    <!-- 时间选择 -->
    <view class="demo-item" @click="showTimePicker">
      <text>选择时间</text>
      <text>{{ timeValue || '请选择' }}</text>
    </view>

    <!-- 日期区间选择 -->
    <view class="demo-item" @click="showRangePicker">
      <text>选择日期区间</text>
      <text>{{ rangeValue || '请选择' }}</text>
    </view>

    <!-- 日期时间选择器 -->
    <wht-datetime-picker
      ref="datePicker"
      mode="datetime"
      :show-seconds="true"
      @confirm="onDateConfirm"
      @cancel="onCancel"
    />

    <!-- 时间选择器 -->
    <wht-datetime-picker
      ref="timePicker"
      mode="time"
      :show-seconds="true"
      @confirm="onTimeConfirm"
      @cancel="onCancel"
    />

    <!-- 日期区间选择器 -->
    <wht-datetime-picker
      ref="rangePicker"
      mode="date-range"
      @confirm="onRangeConfirm"
      @cancel="onCancel"
    />
  </view>
</template>

<script>
export default {
  data() {
    return {
      dateValue: '',
      timeValue: '',
      rangeValue: ''
    }
  },
  methods: {
    // 显示选择器
    showDatePicker() {
      this.$refs.datePicker.show()
    },
    showTimePicker() {
      this.$refs.timePicker.show()
    },
    showRangePicker() {
      this.$refs.rangePicker.show()
    },

    // 确认事件
    onDateConfirm({ value, formatted }) {
      this.dateValue = formatted
      uni.showToast({
        title: '已选择：' + formatted,
        icon: 'none'
      })
    },
    onTimeConfirm({ value, formatted }) {
      this.timeValue = formatted
      uni.showToast({
        title: '已选择：' + formatted,
        icon: 'none'
      })
    },
    onRangeConfirm({ value, formatted }) {
      this.rangeValue = formatted
      uni.showToast({
        title: '已选择：' + formatted,
        icon: 'none'
      })
    },

    // 取消事件
    onCancel() {
      uni.showToast({
        title: '已取消',
        icon: 'none'
      })
    }
  }
}
</script>

<style>
.demo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30rpx;
  margin: 20rpx;
  background-color: #ffffff;
  border-radius: 12rpx;
  box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
}
</style>
```

### 2. 快捷选项使用

```vue
<template>
  <view>
    <view class="demo-item" @click="showQuickPicker">
      <text>快捷日期选择</text>
      <text>{{ quickValue || '请选择' }}</text>
    </view>

    <wht-datetime-picker
      ref="quickPicker"
      mode="date"
      :quick-options="quickOptions"
      @confirm="onQuickConfirm"
    />
  </view>
</template>

<script>
export default {
  data() {
    return {
      quickValue: '',
      quickOptions: [
        {
          label: '今天',
          value: new Date(),
          autoConfirm: true
        },
        {
          label: '昨天',
          value: new Date(Date.now() - 24 * 60 * 60 * 1000)
        },
        {
          label: '一周前',
          value: new Date(Date.now() - 7 * 24 * 60 * 60 * 1000)
        }
      ]
    }
  },
  methods: {
    showQuickPicker() {
      this.$refs.quickPicker.show()
    },
    onQuickConfirm({ value, formatted }) {
      this.quickValue = formatted
      uni.showToast({
        title: '已选择：' + formatted,
        icon: 'none'
      })
    }
  }
}
</script>
```

### 3. 区间选择使用

```vue
<template>
  <view>
    <!-- 日期时间区间 -->
    <view class="demo-item" @click="showDateTimeRange">
      <text>日期时间区间</text>
      <text>{{ dateTimeRange || '请选择' }}</text>
    </view>

    <!-- 日期区间 -->
    <view class="demo-item" @click="showDateRange">
      <text>日期区间</text>
      <text>{{ dateRange || '请选择' }}</text>
    </view>

    <!-- 时间区间 -->
    <view class="demo-item" @click="showTimeRange">
      <text>时间区间</text>
      <text>{{ timeRange || '请选择' }}</text>
    </view>

    <!-- 日期时间区间选择器 -->
    <wht-datetime-picker
      ref="dateTimeRangePicker"
      mode="datetime-range"
      :show-seconds="true"
      @confirm="onDateTimeRangeConfirm"
      @cancel="onCancel"
    />

    <!-- 日期区间选择器 -->
    <wht-datetime-picker
      ref="dateRangePicker"
      mode="date-range"
      @confirm="onDateRangeConfirm"
      @cancel="onCancel"
    />

    <!-- 时间区间选择器 -->
    <wht-datetime-picker
      ref="timeRangePicker"
      mode="time-range"
      :show-seconds="true"
      @confirm="onTimeRangeConfirm"
      @cancel="onCancel"
    />
  </view>
</template>

<script>
export default {
  data() {
    return {
      dateTimeRange: '',
      dateRange: '',
      timeRange: ''
    }
  },
  methods: {
    // 显示选择器
    showDateTimeRange() {
      this.$refs.dateTimeRangePicker.show()
    },
    showDateRange() {
      this.$refs.dateRangePicker.show()
    },
    showTimeRange() {
      this.$refs.timeRangePicker.show()
    },

    // 确认事件处理
    onDateTimeRangeConfirm({ value, formatted }) {
      // value 是日期对象数组 [startDate, endDate]
      // formatted 是格式化后的字符串数组 [startDateString, endDateString]
      this.dateTimeRange = formatted.join(' 至 ')
      uni.showToast({
        title: '已选择：' + this.dateTimeRange,
        icon: 'none'
      })
    },
    onDateRangeConfirm({ value, formatted }) {
      this.dateRange = formatted.join(' 至 ')
      uni.showToast({
        title: '已选择：' + this.dateRange,
        icon: 'none'
      })
    },
    onTimeRangeConfirm({ value, formatted }) {
      this.timeRange = formatted.join(' 至 ')
      uni.showToast({
        title: '已选择：' + this.timeRange,
        icon: 'none'
      })
    },

    // 取消事件
    onCancel() {
      uni.showToast({
        title: '已取消',
        icon: 'none'
      })
    }
  }
}
</script>

<style>
.demo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30rpx;
  margin: 20rpx;
  background-color: #ffffff;
  border-radius: 12rpx;
  box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
}
</style>
```

### 4. 快捷选项使用
{{ ... }}