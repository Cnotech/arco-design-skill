---
name: arco-vue-split
description: "Arco Design Vue 面板分割 Split 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-split>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 面板分割 Split

来源组件：上游 `web-vue/components/split`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-split>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
将一个面板分割成两个可以调整宽度或高度的两部分。用`direction`控制分割方向。




```vue
<template>
  <div>
    <a-split :style="{
        height: '200px',
        width: '100%',
        minWidth: '500px',
        border: '1px solid var(--color-border)'
      }"
      v-model:size="size"
      min="80px"
    >
      <template #first>
        <a-typography-paragraph>Left</a-typography-paragraph>
      </template>
      <template #second>
        <a-typography-paragraph>Right</a-typography-paragraph>
      </template>
    </a-split>
  </div>
</template>
<script>
export default {
  data() {
    return {
      size: 0.5
    }
  }
}
</script>
```

## 示例：面板分割嵌套

### 说明
面板分割可以嵌套使用。




```vue
<template>
<div>
  <a-split :style="{
      height: '200px',
      width: '100%',
      minWidth: '500px',
      border: '1px solid var(--color-border)'
    }"
  >
    <template #first>
      <a-typography-paragraph>Left</a-typography-paragraph>
    </template>
    <template #second>
      <div>
        <a-split direction="vertical" :style="{height: '200px'}">
          <template #first><a-typography-paragraph>Top</a-typography-paragraph></template>
          <template #second><a-typography-paragraph>Bottom</a-typography-paragraph></template>
        </a-split>
      </div>
    </template>
  </a-split>
</div>
</template>
```

## API


### `<split>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|component|分割框的 html 标签|`string`|`'div'`|
|direction|分割的方向|`'horizontal' \| 'vertical'`|`'horizontal'`|
|size **(v-model)**|分割的大小，可以是 0~1 代表百分比，或具体数值的像素，如 300px|`number\|string`|`-`|
|default-size|默认分割的大小，可以是 0~1 代表百分比，或具体数值的像素，如 300px|`number\|string`|`0.5`|
|min|最小阈值，可以是 0~1 代表百分比，或具体数值的像素，如 300px|`number\|string`|`-`|
|max|最大阈值，可以是 0~1 代表百分比，或具体数值的像素，如 300px|`number\|string`|`-`|
|disabled|是否禁用|`boolean`|`false`|
### `<split>` 事件

|事件名|描述|参数|
|---|---|---|
|move-start|开始拖拽之前触发|-|
|moving|拖拽时触发|-|
|move-end|拖拽结束之后触发|-|
### `<split>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|first|第一个面板的内容|-|
|resize-trigger|伸缩杆的内容|-|
|resize-trigger-icon|伸缩杆的图标|-|
|second|第二个面板的内容|-|
