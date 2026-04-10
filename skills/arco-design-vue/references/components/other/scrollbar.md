---
name: arco-vue-scrollbar
description: "Arco Design Vue 滚动条 Scrollbar 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-scrollbar>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 滚动条 Scrollbar

来源组件：上游 `web-vue/components/scrollbar`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-scrollbar>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
滚动条组件基本用法。scrollbar 的默认插槽需要唯一的子元素。




```vue
<template>
  <a-scrollbar style="height:200px;overflow: auto;">
    <div style="height: 2000px;width: 2000px; background-color: var(--color-primary-light-4);">Content</div>
  </a-scrollbar>
</template>
```

## 示例：滚动条类型

### 说明
设置 `type` 属性改变滚动条类型，`track` 类型会显示滚动条轨道。




```vue
<template>
  <a-scrollbar type="track" style="height:200px;overflow: auto;">
    <div style="height: 2000px;width: 2000px; background-color: var(--color-primary-light-4);">Content</div>
  </a-scrollbar>
</template>

<script>
export default {
}
</script>
```


## API

### `<scrollbar>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|类型|`'track' \| 'embed'`|`'embed'`|
|outer-class|外层的类名|`string\|object\|array`|`-`|
|outer-style|外层的样式|`StyleValue`|`-`|
### `<scrollbar>` 事件

|事件名|描述|参数|
|---|---|---|
|scroll|滚动时触发|-|
### `<scrollbar>` 方法

|方法名|描述|参数|返回值|版本|
|---|---|---|---|:---|
|scrollTo|滚动|options: `number \| {left?: number;top?: number}`<br>y: `number`|-||
|scrollTop|纵向滚动|top: `number`|-|2.40.0|
|scrollLeft|横向滚动|left: `number`|-|2.40.0|
