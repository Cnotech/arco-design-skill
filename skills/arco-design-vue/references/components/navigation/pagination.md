---
name: arco-vue-pagination
description: "Arco Design Vue 分页 Pagination 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-pagination>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 分页 Pagination

来源组件：上游 `web-vue/components/pagination`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-pagination>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
分页的基本用法，`total` 属性为必填项。




```vue
<template>
  <a-pagination :total="50"/>
</template>
```

## 示例：更多页码

### 说明
当页码较大时，会使用更多页码的分页样式。




```vue
<template>
  <a-pagination :total="200"/>
</template>
```

## 示例：每页条数

### 说明
通过设置 `show-page-size`， 展示每页条数选择器。




```vue
<template>
  <a-pagination :total="200" show-page-size/>
</template>
```

## 示例：页码跳转

### 说明
通过设置 `show-jumper`，显示页码跳转输入框。




```vue
<template>
  <a-pagination :total="50" show-jumper/>
</template>
```

## 示例：分页尺寸

### 说明
分页分为 `mini`、`small`、`medium`、`large` 四种尺寸。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-radio-group type="button" v-model="size">
      <a-radio value="mini">Mini</a-radio>
      <a-radio value="small">Small</a-radio>
      <a-radio value="medium">Medium</a-radio>
      <a-radio value="large">Large</a-radio>
    </a-radio-group>
    <a-pagination :total="50" :size="size" show-total show-jumper show-page-size />
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const size = ref('medium');

    return {
      size
    }
  },
}
</script>
```

## 示例：简洁模式

### 说明
通过设置 `simple` 属性开启简洁模式。




```vue
<template>
  <a-pagination :total="200" simple/>
</template>
```

## 示例：展示总数

### 说明
通过设置 `show-total` 属性显示数据总数。




```vue
<template>
  <a-pagination :total="200" show-total/>
</template>
```

## 示例：全部展示

### 说明
展示全部配置项。




```vue
<template>
  <a-pagination :total="50" show-total show-jumper show-page-size/>
</template>
```

## 示例：自定义分页按钮

### 说明
可以通过插槽自定义分页按钮内容




```vue
<template>
  <a-pagination :total="200">
    <template #page-item="{ page }">
      - {{page}} -
    </template>
    <template #page-item-step="{ type }">
      <icon-send :style="type==='previous' ? {transform:`rotate(180deg)`} : undefined" />
    </template>
    <template #page-item-ellipsis>
      <icon-sun-fill />
    </template>
  </a-pagination>
</template>
```

## API


### `<pagination>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|total **(必填)**|数据总数|`number`|`-`||
|current **(v-model)**|当前的页数|`number`|`-`||
|default-current|默认的页数（非受控状态）|`number`|`1`||
|page-size **(v-model)**|每页展示的数据条数|`number`|`-`||
|default-page-size|默认每页展示的数据条数（非受控状态）|`number`|`10`||
|disabled|是否禁用|`boolean`|`false`||
|hide-on-single-page|单页时是否隐藏分页|`boolean`|`false`||
|simple|是否为简单模式|`boolean`|`false`||
|show-total|是否显示数据总数|`boolean`|`false`||
|show-more|是否显示更多按钮|`boolean`|`false`||
|show-jumper|是否显示跳转|`boolean`|`false`||
|show-page-size|是否显示数据条数选择器|`boolean`|`false`||
|page-size-options|数据条数选择器的选项列表|`number[]`|`[10, 20, 30, 40, 50]`||
|page-size-props|数据条数选择器的Props|`SelectProps`|`-`||
|size|分页选择器的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|page-item-style|分页按钮的样式|`CSSProperties`|`-`||
|active-page-item-style|当前分页按钮的样式|`CSSProperties`|`-`||
|base-size|计算显示省略的基础个数。显示省略的个数为 `baseSize + 2 * bufferSize`|`number`|`6`||
|buffer-size|显示省略号时，当前页码左右显示的页码个数|`number`|`2`||
|auto-adjust|是否在改变数据条数时调整页码|`boolean`|`true`|2.34.0|
### `<pagination>` 事件

|事件名|描述|参数|
|---|---|---|
|change|页码改变时触发|current: `number`|
|page-size-change|数据条数改变时触发|pageSize: `number`|
### `<pagination>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|total|总数|total: `number`|2.9.0|
|page-item-ellipsis|分页按钮（省略）|-|2.9.0|
|page-item-step|分页按钮（步）|type: `'previous'\|'next'`The type of page item step|2.9.0|
|page-item|分页按钮|page: `number`The page number of the paging button|2.9.0|
