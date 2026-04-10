---
name: arco-vue-input-tag
description: "Arco Design Vue 标签输入框 InputTag 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-input-tag>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 标签输入框 InputTag

来源组件：上游 `web-vue/components/input-tag`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-input-tag>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
标签输入框的基本用法。




```vue
<template>
  <a-input-tag :default-value="['test']" :style="{width:'320px'}" placeholder="Please Enter" allow-clear/>
</template>
```

## 示例：输入框状态

### 说明
输入框有禁用、只读和错误三种状态。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-tag :default-value="['test']" :style="{width:'320px'}" placeholder="Please Enter" disabled/>
    <a-input-tag :default-value="['test']" :style="{width:'320px'}" placeholder="Please Enter" readonly/>
    <a-input-tag :default-value="['test']" :style="{width:'320px'}" placeholder="Please Enter" error/>
  </a-space>
</template>
```

## 示例：最多展示标签数量

### 说明
设置最多展示标签数量。




```vue
<template>
  <a-input-tag :default-value="['one','two','three','four']" :style="{width:'380px'}" placeholder="Please Enter" :max-tag-count="3" allow-clear/>
</template>
```

## 示例：输入框尺寸

### 说明
输入框分为 `mini`、`small`、`medium`、`large` 四种尺寸。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-radio-group type="button" v-model="size">
      <a-radio value="mini">mini</a-radio>
      <a-radio value="small">small</a-radio>
      <a-radio value="medium">medium</a-radio>
      <a-radio value="large">large</a-radio>
    </a-radio-group>
    <a-input-tag :default-value="['one']" :style="{width:'320px'}" placeholder="Please enter something" :size="size" allow-clear />
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

## API


### `<input-tag>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`(string \| number \| TagData)[]`|`-`||
|default-value|默认值（非受控状态）|`(string \| number \| TagData)[]`|`[]`||
|input-value **(v-model)**|输入框的值|`string`|`-`||
|default-input-value|输入框的默认值（非受控状态）|`string`|`''`||
|placeholder|占位符|`string`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|error|是否为错误状态|`boolean`|`false`||
|readonly|是否为只读模式|`boolean`|`false`||
|allow-clear|是否允许清空|`boolean`|`false`||
|size|输入框的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|max-tag-count|最多展示的标签个数，`0` 表示不限制|`number`|`0`||
|retain-input-value|是否保留输入框的内容|`boolean \| { create?: boolean; blur?: boolean }`|`false`||
|format-tag|格式化标签内容|`(data: TagData) => string`|`-`||
|unique-value|是否仅创建唯一的值|`boolean`|`false`|2.15.0|
|field-names|自定义 `TagData` 中的字段|`InputTagFieldNames`|`-`|2.22.0|
|tag-nowrap|标签内容不换行|`boolean`|`false`|2.56.1|
### `<input-tag>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值发生改变时触发|value: `(string \| number \| TagData)[]`<br>ev: `Event`|
|input-value-change|输入值发生改变时触发|inputValue: `string`<br>ev: `Event`|
|press-enter|按下回车键时触发|inputValue: `string`<br>ev: `KeyboardEvent`|
|remove|点击标签的删除按钮时触发|removed: `string \| number`<br>ev: `Event`|
|clear|点击清除按钮时触发|ev: `MouseEvent`|
|focus|输入框获取焦点时触发|ev: `FocusEvent`|
|blur|输入框失去焦点时触发|ev: `FocusEvent`|
### `<input-tag>` 方法

|方法名|描述|参数|返回值|
|---|---|---|---|
|focus|使输入框获取焦点|-|-|
|blur|使输入框失去焦点|-|-|
### `<input-tag>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|tag|输入框标签的显示内容|data: `TagData`|
|prefix|前缀元素|-|
|suffix|后缀元素|-|




### TagData

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|value|标签值|`string \| number`|`-`|
|label|标签内容|`string`|`-`|
|closable|是否可关闭|`boolean`|`false`|
|tagProps|标签属性|`TagProps`|`-`|
