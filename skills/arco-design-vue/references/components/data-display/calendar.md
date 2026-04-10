---
name: arco-vue-calendar
description: "Arco Design Vue 日历 Calendar 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-calendar>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 日历 Calendar

来源组件：上游 `web-vue/components/calendar`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-calendar>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
展示和选择日历




```vue

<template>
  <a-calendar v-model="value" />
  select: {{value}}
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref(new Date('2023-01-01'));

    return {
      value
    }
  },
}
</script>
```

## API


### `<calendar>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|model-value **(v-model)**|绑定值|`date`|`-`|
|default-value|默认值（非受控状态）|`date`|`-`|
|mode|模式|`'month' \| 'year'`|`-`|
|default-mode|默认模式|`'month' \| 'year'`|`'month'`|
|modes|显示的模式|`('month' \| 'year')[]`|`['month', 'year']`|
### `<calendar>` 事件

|事件名|描述|参数|
|---|---|---|
|change|选择的日期改变时触发|date: `Date`|
|panel-change|日期面板改变时触发|date: `Date`|
### `<calendar>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|header|自定义头部内容|year: `number`<br>month: `number`|2.53.0|
|default|自定义单元格内容|year: `number`<br>month: `number`<br>date: `number`|2.53.0|
