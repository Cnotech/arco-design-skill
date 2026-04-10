---
name: arco-vue-time-picker
description: "Arco Design Vue 时间选择器 TimePicker 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-time-picker>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 时间选择器 TimePicker

来源组件：上游 `web-vue/components/time-picker`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-time-picker>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
时间输入器的基础用法。




```vue
<template>
  <a-time-picker style="width: 194px;" />
</template>
```

## 示例：范围选择器

### 说明
时间输入器的范围选择器。




```vue
<template>
  <a-time-picker
    type="time-range"
    @select="(valueString, value) => print('onSelect:', valueString, value)"
    @change="(valueString, value) => print('onChange:', valueString, value)"
    style="width: 252px;" />
</template>
<script>
  export default {
    methods: {
      print(...arg) {
        console.log(...arg);
      }
    }
  }
</script>
```

## 示例：双向绑定

### 说明
支持 `v-model` 进行数据的双向绑定。




```vue
<template>
  <a-time-picker
    style="width: 194px"
    v-model="value"
  />
</template>
<script>
  export default {
    data() {
      return {
        value: null
      }
    }
  }
</script>
```

## 示例：默认值

### 说明
只有默认值的情况，可通过 `defaultValue` 传递。




```vue
<template>
  <a-time-picker
    defaultValue="18:24:23"
    style="width: 194px; marginRight: 24px; marginBottom: 24px"
  />
  <a-time-picker
    type="time-range"
    :defaultValue="['09:24:53', '18:44:33']"
    style="width: 252px; marginBottom: 24px"
  />
</template>
```

## 示例：尺寸

### 说明
有四种尺寸可供选择。




```vue
<template>
  <div style="marginBottom: 20px">
    <a-radio-group v-model="size" type='button'>
      <a-radio value="mini">mini</a-radio>
      <a-radio value="small">small</a-radio>
      <a-radio value="medium">medium</a-radio>
      <a-radio value="large">large</a-radio>
    </a-radio-group>
  </div>
  <a-time-picker style="width: 194px;" :size="size" />
</template>
<script>
  export default {
    data() {
      return {
        size: 'small'
      }
    }
  }
</script>
```

## 示例：禁用

### 说明
禁用状态。




```vue
<template>
  <a-time-picker disabled style="margin: 0 24px 24px 0;" />
  <a-time-picker type="time-range" disabled style="width: 252px; margin: 0 24px 24px 0;" />
</template>
```

## 示例：禁用部分时间选项

### 说明
通过设置 `disabledHours` `disabledMinutes` `disabledSeconds`，可以禁用 时 / 分 / 秒的部分选项。




```vue
<template>
  <a-time-picker
    style="width: 194px; margin: 0 24px 24px 0;"
    :disabledHours="() => [1, 2, 4, 14]"
    :disabledMinutes="() => [1, 2, 3, 4, 14, 15, 16, 20, 50]"
    :disabledSeconds="() => [1, 2, 3, 4, 5, 6, 7, 10, 14, 60]"
  />
  <a-time-picker
    type="time-range"
    style="width: 252px; margin: 0 24px 24px 0;"
    :disabledHours="() => [1, 2, 4, 14]"
    :disabledMinutes="() => [1, 2, 3, 4, 14, 15, 16, 20, 50]"
    :disabledSeconds="() => [1, 2, 3, 4, 5, 6, 7, 10, 14, 60]"
  />
</template>
```

## 示例：跳过确认

### 说明
跳过确认步骤，直接点击选择时间。




```vue
<template>
  <a-time-picker
    disableConfirm
    style="width: 194px; margin: 0 24px 24px 0;"
  />
  <a-time-picker
    type="time-range"
    disableConfirm
    style="width: 252px; margin: 0 24px 24px 0;"
  />
</template>
```

## 示例：定制格式

### 说明
通过设置 `format`，可以定制需要显示的时、分、秒。




```vue
<template>
  <a-time-picker format="HH:mm" :defaultValue="defaultValue" style="width: 130px;" />
</template>
<script>
export default {
  data() {
    return {
      defaultValue: '09:24'
    }
  }
}
</script>
```

## 示例：定制步长

### 说明
通过设置 `step`，可以定制需要显示的时、分、秒的步长。




```vue
<template>
  <a-time-picker
    defaultValue="10:25:30"
    :step="{
      hour: 2,
      minute: 5,
      second: 10,
    }"
    style="width: 194px;" />
</template>
```

## 示例：附加内容

### 说明
选择框底部显示自定义的内容。




```vue
<template>
  <a-time-picker style="width: 194px;">
    <template #extra>
      Extra Footer
    </template>
  </a-time-picker>
</template>
```

## 示例：十二小时制

### 说明
通过设置 `use12Hours`，可以定制需要显示的时、分、秒。




```vue
<template>
  <a-time-picker
    use12Hours
    defaultValue="12:20:20 AM"
    format="hh:mm:ss A"
    style="width: 194px; margin: 0 24px 24px 0;"
  />
  <a-time-picker
    use12Hours
    defaultValue="09:20:20 pm"
    format="hh:mm:ss a"
    style="width: 194px; margin: 0 24px 24px 0;"
  />
  <a-time-picker
    use12Hours
    defaultValue="2:20 AM"
    format="h:mm A"
    style="width: 194px; margin: 0 24px 24px 0;"
  />
  <a-time-picker
    type="time-range"
    use12Hours
    :defaultValue="['12:20:20 AM', '08:30:30 PM']"
    format="hh:mm:ss A"
    style="width: 300px; margin: 0 24px 24px 0;"
  />
</template>
```

## API


### `<time-picker>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|选择器类型|`'time' \| 'time-range'`|`'time'`|
|model-value **(v-model)**|绑定值|`string \| number \| Date \| Array<string \| number \| Date>`|`-`|
|default-value|默认值|`string \| number \| Date \| Array<string \| number \| Date>`|`-`|
|disabled|是否禁用|`boolean`|`false`|
|allow-clear|是否允许清除|`boolean`|`true`|
|readonly|是否为只读模式|`boolean`|`false`|
|error|是否为错误状态|`boolean`|`false`|
|format|展示日期的格式，参考[字符串解析格式](#字符串解析格式)|`string`|`'HH:mm:ss'`|
|placeholder|提示文案|`string \| string[]`|`-`|
|size|输入框尺寸|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`|
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`-`|
|use12-hours|12 小时制|`boolean`|`false`|
|step|设置 时 / 分 / 秒 的选择间隔|`{  hour?: number;  minute?: number;  second?: number;}`|`-`|
|disabled-hours|禁用的部分小时选项|`() => number[]`|`-`|
|disabled-minutes|禁用的部分分钟选项|`(selectedHour?: number) => number[]`|`-`|
|disabled-seconds|禁用的部分秒数选项|`(selectedHour?: number, selectedMinute?: number) => number[]`|`-`|
|hide-disabled-options|隐藏禁止选择的选项|`boolean`|`false`|
|disable-confirm|禁用确认步骤，开启后直接点选时间不需要点击确认按钮|`boolean`|`false`|
|position|弹出的位置|`'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br'`|`'bl'`|
|popup-visible **(v-model)**|控制弹出框打开或者关闭|`boolean`|`-`|
|default-popup-visible|弹出框默认打开或者关闭|`boolean`|`false`|
|trigger-props|可以传入 `Trigger` 组件的参数|`TriggerProps`|`-`|
|unmount-on-close|是否在关闭后销毁 dom 结构|`boolean`|`false`|
### `<time-picker>` 事件

|事件名|描述|参数|
|---|---|---|
|change|组件值发生改变|timeString: `string \| Array<string \| undefined> \| undefined`<br>time: `date \| Array<date \| undefined> \| undefined`|
|select|选择时间但未触发组件值变化|timeString: `string \| Array<string \| undefined>`<br>time: `Date \| Array<Date \| undefined>`|
|clear|点击清除按钮|-|
|popup-visible-change|弹出框展开和收起|visible: `boolean`|
### `<time-picker>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|prefix|输入框前缀|-|2.41.0|
|suffix-icon|输入框后缀图标|-||
|extra|额外的页脚|-||



### 字符串解析格式

格式|输出|描述
---|---|---:
`YY`|21|两位数的年份
`YYYY`|2021|四位数年份
`M`|1-12|月份，从 1 开始
`MM`|01-12|月份，两位数
`MMM`|Jan-Dec|缩写的月份名称
`MMMM`|January-December|完整的月份名称
`D`|1-31|月份里的一天
`DD`|01-31|月份里的一天，两位数
`d`|0-6|一周中的一天，星期天是 0
`dd`|Su-Sa|最简写的一周中一天的名称
`ddd`|Sun-Sat|简写的一周中一天的名称
`dddd`|Sunday-Saturday|一周中一天的名称
`H`|0-23|小时
`HH`|00-23|小时，两位数
`h`|1-12|小时, 12 小时制
`hh`|01-12|小时, 12 小时制, 两位数
`m`|0-59|分钟
`mm`|00-59|分钟，两位数
`s`|0-59|秒
`ss`|00-59|秒，两位数
`S`|0-9|数百毫秒，一位数
`SS`|00-99|几十毫秒，两位数
`SSS`|000-999|毫秒，三位数字
`Z`|-5:00|UTC 的偏移量
`ZZ`|-0500|UTC 的偏移量，数字前面加上 0
`A`|AM PM|-
`a`|am pm|-
`Do`|1st... 3st|带序号的月份中的某天
`X`|1410715640.579|Unix 时间戳
`x`|1410715640579|Unix 毫秒时间戳
