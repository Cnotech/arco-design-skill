---
name: arco-vue-input
description: "Arco Design Vue 输入框 Input 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-input>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 输入框 Input

来源组件：上游 `web-vue/components/input`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-input>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
输入框的基本用法。




```vue
<template>
  <a-space>
    <a-input :style="{width:'320px'}" placeholder="Please enter something" allow-clear />
    <a-input :style="{width:'320px'}" default-value="content" placeholder="Please enter something" allow-clear />
  </a-space>
</template>
```

## 示例：输入框状态

### 说明
输入框可以设置禁用和错误状态。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input :style="{width:'320px'}" placeholder="Disabled status" disabled/>
    <a-input :style="{width:'320px'}" default-value="Disabled" placeholder="Disabled status" disabled/>
    <a-input :style="{width:'320px'}" placeholder="Error status" error/>
  </a-space>
</template>
```

## 示例：输入框尺寸

### 说明
输入框定义了四种默认尺寸 `mini, small, medium, large` ，分别为 `24px, 28px, 32px, 36px` 。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-radio-group type="button" v-model="size">
      <a-radio value="mini">mini</a-radio>
      <a-radio value="small">small</a-radio>
      <a-radio value="medium">medium</a-radio>
      <a-radio value="large">large</a-radio>
    </a-radio-group>
    <a-input :style="{width:'320px'}" placeholder="Please enter something" :size="size" allow-clear />
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

## 示例：前缀与后缀

### 说明
通过指定 `prefix` 和 `suffix` 插槽来在输入框内添加前缀和后缀。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input :style="{width:'320px'}" placeholder="Please enter something" allow-clear>
      <template #prefix>
        <icon-user />
      </template>
    </a-input>
    <a-input :style="{width:'320px'}" placeholder="Please enter something" allow-clear>
      <template #suffix>
        <icon-info-circle />
      </template>
    </a-input>
  </a-space>
</template>
```

## 示例：前置、后置标签

### 说明
通过指定 `prepend` 和 `append` 插槽在输入框前后添加元素。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input :style="{width:'320px'}" placeholder="Please enter something" allow-clear>
      <template #prepend>
        +86
      </template>
    </a-input>
    <a-input :style="{width:'320px'}" placeholder="Please enter something" allow-clear>
      <template #append>
        RMB
      </template>
    </a-input>

    <a-input :style="{width:'320px'}" placeholder="Please enter something" allow-clear prepend="+86">
    </a-input>
    <a-input :style="{width:'320px'}" placeholder="Please enter something" allow-clear append="RMB">
    </a-input>
  </a-space>
</template>
```

## 示例：字数统计

### 说明
设置 `max-length` 可以限制最大字数，配合 `show-word-limit` 可以显示字数统计。




```vue
<template>
  <a-space direction="vertical" size="large" fill>
    <a-input :style="{width:'320px'}" placeholder="Please enter something" :max-length="10" allow-clear show-word-limit />
    <a-input :style="{width:'320px'}" placeholder="Please enter something" :max-length="{length:10,errorOnly:true}" allow-clear show-word-limit />
  </a-space>
</template>
```

## 示例：输入框组合

### 说明
通过 `input-group` 可以组合使用输入框。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-group>
      <a-input :style="{width:'160px'}" placeholder="first" />
      <a-input :style="{width:'160px'}" placeholder="second" />
    </a-input-group>
    <a-input-group>
      <a-select :options="['Option1','Option2','Option3']" :style="{width:'160px'}" placeholder="first" />
      <a-input :style="{width:'160px'}" placeholder="second" />
    </a-input-group>
  </a-space>
</template>
```

## 示例：搜索框

### 说明
带有搜索按钮的输入框，用于内容检索。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-search :style="{width:'320px'}" placeholder="Please enter something"/>
    <a-input-search :style="{width:'320px'}" placeholder="Please enter something" search-button/>
  </a-space>
</template>
```

## 示例：自定义搜索按钮

### 说明
自定义搜索按钮的内容




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-search :style="{width:'320px'}" placeholder="Please enter something" button-text="Search" search-button/>
    <a-input-search :style="{width:'320px'}" placeholder="Please enter something" search-button>
      <template #button-icon>
        <icon-search/>
      </template>
      <template #button-default>
        Search
      </template>
    </a-input-search>
  </a-space>
</template>
```

## 示例：搜索框（加载中）

### 说明
通过 `loading` 属性可以让搜索框展示加载中状态。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-search :style="{width:'320px'}" placeholder="Please enter something" loading />
    <a-input-search :style="{width:'320px'}" placeholder="Please enter something" search-button loading />
  </a-space>
</template>
```

## 示例：密码输入框

### 说明
用于输入密码。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-switch v-model="visibility" />
    <a-input-password
      v-model:visibility="visibility"
      placeholder="Please enter something"
      :style="{width:'320px'}"
      :defaultVisibility="false"
      allow-clear
    />
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visibility = ref(true);

    return {
      visibility
    }
  },
}
</script>
```

## API


### `<input>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`string`|`-`||
|default-value|默认值（非受控状态）|`string`|`''`||
|size|输入框大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|allow-clear|是否允许清空输入框|`boolean`|`false`||
|disabled|是否禁用|`boolean`|`false`||
|readonly|是否为只读状态|`boolean`|`false`||
|error|是否为错误状态|`boolean`|`false`||
|placeholder|提示文字|`string`|`-`||
|max-length|输入值的最大长度，errorOnly 属性在 2.12.0 版本添加|`number \| { length: number; errorOnly?: boolean }`|`0`||
|show-word-limit|是否显示字数统计|`boolean`|`false`||
|word-length|字符长度的计算方法|`(value: string) => number`|`-`||
|word-slice|字符截取方法，同 wordLength 一起使用|`(value: string, maxLength: number) => string`|`-`|2.12.0|
|input-attrs|内部 input 元素的属性|`object`|`-`|2.27.0|
|prepend|前置标签|`string`|`-`|2.57.0|
|append|后置标签|`string`|`-`|2.57.0|
### `<input>` 事件

|事件名|描述|参数|
|---|---|---|
|input|用户输入时触发|value: `string`<br>ev: `Event`|
|change|仅在输入框失焦或按下回车时触发|value: `string`<br>ev: `Event`|
|press-enter|用户按下回车时触发|ev: `KeyboardEvent`|
|clear|用户点击清除按钮时触发|ev: `MouseEvent`|
|focus|输入框获取焦点时触发|ev: `FocusEvent`|
|blur|输入框失去焦点时触发|ev: `FocusEvent`|
### `<input>` 方法

|方法名|描述|参数|返回值|
|---|---|---|---|
|focus|使输入框获取焦点|-|-|
|blur|使输入框失去焦点|-|-|
### `<input>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|append|后置标签|-|
|prepend|前置标签|-|
|suffix|后缀元素|-|
|prefix|前缀元素|-|








### `<input-password>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|visibility **(v-model)**|是否可见，受控属性|`boolean`|`-`|
|default-visibility|默认是否可见，非受控|`boolean`|`true`|
|invisible-button|是否显示可见按钮|`boolean`|`true`|
### `<input-password>` 事件

|事件名|描述|参数|
|---|---|---|
|visibility-change|visibility 改变时触发|visible: `boolean`|




### `<input-search>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|search-button|是否为后置按钮模式|`boolean`|`false`||
|loading|是否为加载中状态|`boolean`|`false`||
|disabled|是否禁用|`boolean`|`false`||
|size|输入框大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|button-text|搜索按钮的文字，使用后会替换原本的图标|`string`|`-`|2.16.0|
|button-props|搜索按钮的属性|`ButtonProps`|`-`||
### `<input-search>` 事件

|事件名|描述|参数|
|---|---|---|
|search|单击搜索按钮时触发|value: `string`<br>ev: `MouseEvent`|
