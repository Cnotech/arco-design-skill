---
name: arco-vue-empty
description: "Arco Design Vue 空状态 Empty 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-empty>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 空状态 Empty

来源组件：上游 `web-vue/components/empty`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-empty>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
空状态组件的基本用法。




```vue
<template>
  <a-empty />
</template>
```

## 示例：自定义图片和文案

### 说明
通过 `image` 插槽自定义图标、图片，或通过内容修改文案。




```vue
<template>
  <a-empty>
    <template #image>
      <icon-exclamation-circle-fill />
    </template>
    No data, please reload!
  </a-empty>
</template>

<script>
import { IconExclamationCircleFill } from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconExclamationCircleFill
  },
}
</script>
```

## API


### `<empty>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|description|描述内容|`string`|`-`||
|img-src|自定义图片的地址|`string`|`-`||
|in-config-provider|是否在 ConfigProvider 中使用|`boolean`|`false`|2.47.0|
### `<empty>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|image|图片/图标|-|
