---
name: arco-vue-spin
description: "Arco Design Vue 加载中 Spin 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-spin>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 加载中 Spin

来源组件：上游 `web-vue/components/spin`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-spin>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
用于展示加载中的状态。




```vue
<template>
  <a-spin />
</template>
```

## 示例：不同尺寸

### 说明
设置 `size` 可以得到不同尺寸的加载图标。




```vue
<template>
  <a-space size="large">
    <a-spin />
    <a-spin :size="28"/>
    <a-spin :size="32"/>
  </a-space>
</template>
```

## 示例：点类型指示符

### 说明
通过 `dot` 属性，可以展示点类型的指示符。




```vue

<template>
  <a-spin dot />
</template>
```

## 示例：容器中

### 说明
可以给任意内容添加加载中指示符。




```vue
<template>
  <a-spin :loading="loading" tip="This may take a while...">
    <a-card title="Arco Card">
      ByteDance's core product, Toutiao ('Headlines'), is a content platform in China and around
      the world. Toutiao started out as a news recommendation engine and gradually evolved into
      a platform delivering content in various formats.
    </a-card>
  </a-spin>
</template>

<script>
export default {
  data() {
    return {
      loading: true
    }
  }
}
</script>
```

## 示例：添加描述文案

### 说明
通过 `tip` 属性添加描述文案。




```vue
<template>
  <a-spin tip="This may take a while..."/>
</template>
```

## 示例：自定义图标

### 说明
通过 `#icon` 插槽可以自定义图标。




```vue
<template>
  <a-spin>
    <template #icon>
      <icon-sync />
    </template>
  </a-spin>
</template>

<script>
import { IconSync } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconSync }
};
</script>
```

## API


### `<spin>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|size|尺寸|`number`|`-`|
|loading|是否为加载中状态（仅在容器模式下生效）|`boolean`|`false`|
|dot|是否使用点类型的动画|`boolean`|`false`|
|tip|提示内容|`string`|`-`|
|hide-icon|是否隐藏图标|`boolean`|`false`|
### `<spin>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|tip|自定义提示内容|-|
|element|自定义元素|-|
|icon|自定义图标（自动旋转）|-|
