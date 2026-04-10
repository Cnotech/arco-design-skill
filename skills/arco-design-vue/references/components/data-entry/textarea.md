---
name: arco-vue-textarea
description: "Arco Design Vue 文本域 Textarea 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-textarea>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 文本域 Textarea

来源组件：上游 `web-vue/components/textarea`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-textarea>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
可以用于多行输入。




```vue
<template>
  <a-textarea placeholder="Please enter something" allow-clear/>
</template>
```

## 示例：文本域状态

### 说明
文本域可以设置禁用和错误状态。




```vue
<template>
  <a-space direction="vertical" size="large" style="width: 100%">
    <a-textarea placeholder="Disabled status" disabled/>
    <a-textarea placeholder="Error status" error/>
  </a-space>
</template>
```

## 示例：字数统计

### 说明
设置 `max-length` 可以限制最大字数，配合 `show-word-limit` 可以显示字数统计。




```vue
<template>
  <a-space direction="vertical" size="large" fill>
    <a-textarea placeholder="Please enter something" :max-length="10" allow-clear show-word-limit />
    <a-textarea placeholder="Please enter something" :max-length="{length:10,errorOnly:true}" allow-clear
                show-word-limit />
  </a-space>
</template>
```

## 示例：自适应高度

### 说明
通过设置 `auto-size`，可以让文本框自适应输入内容。




```vue
<template>
  <a-textarea default-value="This is the contents of the textarea. This is the contents of the textarea. This is the contents of the textarea." auto-size />
  <a-textarea default-value="This is the contents of the textarea. This is the contents of the textarea. This is the contents of the textarea." :auto-size="{
    minRows:2,
    maxRows:5
  }" style="margin-top: 20px"/>
</template>
```

## API


### `<textarea>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`string`|`-`||
|default-value|默认值（非受控状态）|`string`|`''`||
|placeholder|提示文字|`string`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|error|是否为错误状态|`boolean`|`false`||
|max-length|输入值的最大长度，errorOnly 属性在 2.12.0 版本添加|`number \| { length: number; errorOnly?: boolean }`|`0`||
|show-word-limit|是否显示字数统计|`boolean`|`false`||
|allow-clear|是否允许清空文本域|`boolean`|`false`||
|auto-size|是否让文本框自适应内容高度|`boolean \| { minRows?: number; maxRows?: number }`|`false`||
|word-length|字符长度的计算方法|`(value: string) => number`|`-`||
|word-slice|字符截取方法，同 wordLength 一起使用|`(value: string, maxLength: number) => string`|`-`|2.12.0|
|textarea-attrs|透传给 textarea 的属性|`Record<string, any>`|`-`||
### `<textarea>` 事件

|事件名|描述|参数|
|---|---|---|
|input|用户输入时触发|value: `string`<br>ev: `Event`|
|change|仅在文本框失焦时触发|value: `string`<br>ev: `Event`|
|clear|点击清除按钮时触发|ev: `MouseEvent`|
|focus|文本框获取焦点时触发|ev: `FocusEvent`|
|blur|文本框失去焦点时触发|ev: `FocusEvent`|
### `<textarea>` 方法

|方法名|描述|参数|返回值|版本|
|---|---|---|---|:---|
|focus|使输入框获取焦点|-|-|2.24.0|
|blur|使输入框失去焦点|-|-|2.24.0|
