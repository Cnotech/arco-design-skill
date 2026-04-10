---
name: arco-vue-verification-code
description: "Arco Design Vue 验证码输入 VerificationCode 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-verification-code>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 验证码输入 VerificationCode

来源组件：上游 `web-vue/components/verification-code`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-verification-code>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
验证码输入框的基本用法。




```vue
<template>
  <a-verification-code v-model="value" style="width: 300px" @finish="onFinish" />
</template>

<script setup>
import { ref } from 'vue';
import { Message} from '@arco-design/web-vue';

const value = ref('654321');
const onFinish = (value) => Message.info(`Verification code: ${value}`);
</script>
```
## 示例：不同状态

### 说明
禁用状态、只读状态、错误状态。




```vue
<template>
  <a-space direction="vertical">
    <a-space>
      <a-typography-text style="width: 80px">Disabled:</a-typography-text>
      <a-verification-code defaultValue="123456" style="width: 300px" disabled />
    </a-space>
    <a-space>
      <a-typography-text  style="width: 80px">Readonly:</a-typography-text>
      <a-verification-code defaultValue="123456" style="width: 300px" readonly />
    </a-space>
    <a-space>
      <a-typography-text style="width: 80px">Error:</a-typography-text>
      <a-verification-code defaultValue="123456" style="width: 300px" error />
    </a-space>
  </a-space>
</template>
```
## 示例：密码模式

### 说明
指定 `masked = true`可开启密码模式




```vue
<template>
  <a-verification-code defaultValue="123" style="width: 300px"  masked @finish="onFinish" />
</template>

<script setup>
import { Message} from '@arco-design/web-vue';

const onFinish = (value) => Message.info(`Verification code: ${value}`);
</script>
```
## 示例：自定义分隔符

### 说明
指定 `separator` 可以自定义渲染分隔符。




```vue
<template>
  <a-verification-code
    style="width: 400px"
    :length="9"
    :separator="(index) => (index + 1) % 3 || index > 7 ? null : '-'"
    @finish="(value) => Message.info(`Verification code: ${value}`)"
  />
</template>

<script setup>
import { Message} from '@arco-design/web-vue';
</script>
```
## 示例：配合表单使用

### 说明
配合表单使用实现校验。




```vue
<template>
  <a-form ref="formRef" :model="form" style="width: 300px">
    <a-form-item
      field="code"
      label="code"
      :rules="[
        {required:true,message:'Verification code is required'},
        {minLength:6, message:'Verification code is incomplete'},
        { match: /^\d+$/, message: 'Must be numeric' },
      ]"
    >
      <a-verification-code v-model="form.code" style="width: 300px" @finish="onFinish" />
    </a-form-item>
    <a-form-item>
      <a-button style="width: 60px" type='primary' size='large' htmlType='submit'>Submit</a-button>
    </a-form-item>
  </a-form>
</template>

<script setup>
import { ref } from 'vue';
import { Message} from '@arco-design/web-vue';

const value = ref('654321');
const formRef = ref(null);
const form = ref({
  code: '',
})
const onFinish = (value) => Message.info(`Verification code: ${value}`);
</script>
```
## 示例：格式化输入

### 说明
通过 `formatter` 校验输入。此外，可以返回非布尔类型来将用户输入的字符串为特定的格式。




```vue
<template>
  <a-space direction="vertical">
    <a-verification-code
      defaultValue='123456'
      style="width: 300px"
      :formatter="(inputValue) =>  /^\d*$/.test(inputValue) ? inputValue : false"
    />
    <a-verification-code
      defaultValue='abcdef'
      style="width: 300px"
      :formatter="(inputValue) => /^[a-zA-Z]*$/.test(inputValue) ? inputValue.toUpperCase() : ''"
    />
  </a-space>
</template>
```

## API


### `<verification-code>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|model-value **(v-model)**|绑定值|`string`|`-`|
|default-value|默认值（非受控状态）|`string`|`''`|
|length|验证码的长度，根据长度渲染对应个数的输入框|`number`|`6`|
|size|输入框大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`|
|disabled|是否禁用|`boolean`|`false`|
|masked|是否密码模式|`boolean`|`false`|
|readonly|只读|`boolean`|`false`|
|error|是否为错误状态|`boolean`|`false`|
|separator|分隔符。可在不同索引的输入框后自定义渲染分隔符|`(index: number, character: string) => VNode`|`-`|
|formatter|格式化函数，当用户输入值改变时触发|`(inputValue: string, index: number, value: string) => string \| boolean`|`-`|
### `<verification-code>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值发生改变时触发|value: ` string `|
|finish|填充完成时触发|value: ` string `|
|input|输入时触发|inputValue: ` string `<br>index: ` number `<br>ev: `Event`|
