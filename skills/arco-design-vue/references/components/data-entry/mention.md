---
name: arco-vue-mention
description: "Arco Design Vue 提及 Mention 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-mention>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 提及 Mention

来源组件：上游 `web-vue/components/mention`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-mention>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
用于在输入中提及某人或某事，常用于发布、聊天或评论功能。




```vue
<template>
  <a-space direction="vertical" size="large" style="width: 100%">
    <a-mention v-model="value" :data="['Bytedance', 'Bytedesign', 'Bytenumner']" placeholder="enter something" />
    <a-mention v-model="text" :data="['Bytedance', 'Bytedesign', 'Bytenumner']" type="textarea" placeholder="enter something" />
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref('');
    const text = ref('');

    return {
      value,
      text
    }
  }
}
</script>
```

## 示例：自定义触发字符

### 说明
指定 `prefix` 来自定义触发字符。默认为 `@`，可以自定义为任意字符。




```vue
<template>
  <a-space direction="vertical" size="large" style="width: 100%">
    <a-mention :data="['Bytedance', 'Bytedesign', 'Bytenumner']" placeholder="input @" />
    <a-mention :data="['Bytedance', 'Bytedesign', 'Bytenumner']" prefix="#" placeholder="input #" />
    <a-mention :data="['Bytedance', 'Bytedesign', 'Bytenumner']" prefix="$" placeholder="input $" />
  </a-space>
</template>
```

## API


### `<mention>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`string`|`-`||
|default-value|默认值（非受控状态）|`string`|`''`||
|data|用于自动补全的数据|`(string \| number \| SelectOptionData \| SelectOptionGroup)[]`|`[]`||
|prefix|触发自动补全的关键字|`string \| string[]`|`'@'`||
|split|选中项的前后分隔符|`string`|`' '`||
|type|输入框或文本域|`'input' \| 'textarea'`|`'input'`||
|disabled|是否禁用|`boolean`|`false`||
|allow-clear|是否允许清空输入框|`boolean`|`false`|2.23.0|
### `<mention>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|change|值发生改变时触发|value: `string`||
|search|动态搜索时触发，2.47.0 版本增加 prefix 参数|value: `string`<br>prefix: `string`||
|select|选择下拉选项时触发|value: `string \| number \| Record<string, any> \| undefined`||
|clear|用户点击清除按钮时触发|-|2.23.0|
|focus|文本框获取焦点时触发|ev: `FocusEvent`|2.42.0|
|blur|文本框失去焦点时触发|ev: `FocusEvent`|2.42.0|
### `<mention>` 方法

|方法名|描述|参数|返回值|版本|
|---|---|---|---|:---|
|focus|使输入框获取焦点|-|-|2.24.0|
|blur|使输入框失去焦点|-|-|2.24.0|
### `<mention>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|option|选项内容|data: `OptionInfo`|2.13.0|
