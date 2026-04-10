---
name: arco-vue-color-picker
description: "Arco Design Vue 颜色选择器 ColorPicker 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-color-picker>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 颜色选择器 ColorPicker

来源组件：上游 `web-vue/components/color-picker`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-color-picker>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
基本用法




```vue
<template>
  <a-space>
    <a-color-picker  v-model="value" />
    <a-color-picker defaultValue="#165DFF" showText disabledAlpha/>
  </a-space>
</template>

<script setup>
import { ref } from 'vue';
const value = ref('#165DFF')
</script>
```
## 示例：尺寸

### 说明
颜色选择器定义了四种尺寸（`mini`,`small`, `medium`, `large`），分别为 24px，28px，32px，36px。




```vue
<template>
  <a-space>
    <a-color-picker defaultValue="#165DFF" size="mini" />
    <a-color-picker defaultValue="#165DFF" size="small" />
    <a-color-picker defaultValue="#165DFF" size="medium" />
    <a-color-picker defaultValue="#165DFF" size="large" />
  </a-space>
</template>
```
## 示例：禁用

### 说明
设置 `disabled` 禁用选择器。




```vue
<template>
  <a-space>
    <a-color-picker defaultValue="#165DFF" disabled />
    <a-color-picker defaultValue="#165DFF" showText disabled />
  </a-space>
</template>
```
## 示例：颜色格式

### 说明
通过 `format` 设置颜色值的格式，支持 `hex` 和 `rgb`。




```vue
<template>
  <a-space direction="vertical">
    <a-radio-group type="button" v-model="format">
      <a-radio v-for="item in formatList" :value="item">{{item}}</a-radio>
    </a-radio-group>
    <a-color-picker defaultValue="#165DFF" :format="format" showText />
  </a-space>
</template>

<script setup>
import { ref } from 'vue';

const format = ref('hex')
const formatList = ['hex', 'rgb']
</script>
```
## 示例：预设颜色和历史颜色

### 说明
通过 `showPreset` 和 `showHistory` 开启预设颜色和历史颜色区域。历史颜色需要用户自行控制展示内容。




```vue
<template>
  <a-color-picker
    defaultValue="#165DFF"
    :historyColors="history"
    showHistory
    showPreset
    @popup-visible-change="addHistory"
  />
</template>

<script setup>
import { ref } from 'vue';

const history = ref(['#165DFF'])
const addHistory = (visible, color) => {
  if (!visible) {
    const index = history.value.indexOf(color);
    if (index !== -1) {
      history.value.splice(index, 1);
    }
    history.value.unshift(color);
  }
}
</script>
```
## 示例：触发器

### 说明
可以通过 `trigger-props` 设置触发器的所有属性。




```vue
<template>
  <a-space direction="vertical">
    <a-switch v-model="triggerProps.popupVisible">
      <template #checked> ON </template>
      <template #unchecked>OFF</template>
    </a-switch>
    <a-color-picker defaultValue="#165DFF" :trigger-props="triggerProps" />
  </a-space>
</template>

<script setup>
import { ref } from 'vue';

const triggerProps = ref({
  popupVisible: false,
  unmountOnClose: true,
  renderToBody: false,
  position: 'rt'
})
</script>
```
## 示例：自定义触发元素

### 说明
自定义触发元素。




```vue
<template>
  <a-space>
    <a-color-picker v-model="value" size="mini" >
      <a-tag :color="value">
        <template #icon>
          <icon-bg-colors style="color: #fff" />
        </template>
        {{value}}
      </a-tag>
    </a-color-picker>
  </a-space>
</template>

<script setup>
import { ref } from 'vue';

const value = ref('#165DFF');
</script>
```
## 示例：只使用面板

### 说明
只用颜色选择面板。




```vue
<template>
  <a-space :size="32">
    <a-color-picker defaultValue="#165DFF" hideTrigger showHistory showPreset/>
    <a-color-picker defaultValue="#12D2AC" disabled hideTrigger showPreset/>
  </a-space>
</template>
```

## API


### `<color-picker>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|model-value **(v-model)**|绑定值|`string`|`-`|
|default-value|默认值（非受控状态）|`string`|`-`|
|format|颜色值的格式|`'hex' \| 'rgb'`|`-`|
|size|尺寸|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`|
|show-text|显示颜色值|`boolean`|`false`|
|show-history|显示历史颜色|`boolean`|`false`|
|show-preset|显示预设颜色|`boolean`|`false`|
|disabled|禁用|`boolean`|`false`|
|disabled-alpha|禁用透明通道|`boolean`|`false`|
|hide-trigger|没有触发元素，只显示颜色面板|`boolean`|`false`|
|trigger-props|接受所有 [Trigger](/vue/component/trigger) 组件的Props|`Partial<TriggerProps>`|`-`|
|history-colors|历史颜色的颜色数组|`string[]`|`-`|
|preset-colors|预设颜色的颜色数组|`string[]`|`() => colors`|
### `<color-picker>` 事件

|事件名|描述|参数|
|---|---|---|
|change|颜色值改变时触发|value: `string`|
|popup-visible-change|颜色面板展开和收起时触发|visible: `boolean`<br>value: `string`|
