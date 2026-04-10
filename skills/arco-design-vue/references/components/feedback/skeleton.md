---
name: arco-vue-skeleton
description: "Arco Design Vue 骨架屏 Skeleton 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-skeleton>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 骨架屏 Skeleton

来源组件：上游 `web-vue/components/skeleton`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-skeleton>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
骨架屏组件提供 `<a-skeleton-line>` 和 `<a-skeleton-shape>` 两种组件，用户可根据需要组合使用。




```vue
<template>
  <a-skeleton>
    <a-space direction="vertical" :style="{width:'100%'}" size="large">
      <a-skeleton-line :rows="3" />
      <a-skeleton-shape />
    </a-space>
  </a-skeleton>
</template>
```

## 示例：图形骨架屏

### 说明
图形骨架屏分为 `square` - **正方形（默认）**、 `circle` - **圆形**两种形状，并提供 `small`、`medium`、`large` 三种尺寸。




```vue
<template>
  <a-skeleton>
    <a-space size="large">
      <a-skeleton-shape size="small" />
      <a-skeleton-shape />
      <a-skeleton-shape size="large" />
      <a-skeleton-shape shape="circle" size="small" />
      <a-skeleton-shape shape="circle" />
      <a-skeleton-shape shape="circle" size="large" />
    </a-space>
  </a-skeleton>
</template>
```

## 示例：动画

### 说明
通过设置 `animation` 属性，让骨架屏显示动画效果。




```vue
<template>
  <a-space direction="vertical" size="large" :style="{width:'100%'}">
    <a-space>
      <span>Animation</span>
      <a-switch v-model="animation" />
    </a-space>
    <a-skeleton :animation="animation">
      <a-space direction="vertical" :style="{width:'100%'}" size="large">
        <a-skeleton-line :rows="3" />
        <a-skeleton-shape />
      </a-space>
    </a-skeleton>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const animation = ref(true);

    return {
      animation
    }
  },
}
</script>
```

## API


### `<skeleton>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|loading|是否展示骨架屏（加载中状态）|`boolean`|`true`|
|animation|是否开启骨架屏动画|`boolean`|`false`|




### `<skeleton-line>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|rows|展示的行数|`number`|`1`|
|widths|线型骨架的宽度|`Array<number \| string>`|`[]`|
|line-height|线型骨架的行高|`number`|`20`|
|line-spacing|线型骨架的行间距|`number`|`15`|




### `<skeleton-shape>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|shape|图形骨架的形状|`'square' \| 'circle'`|`'square'`|
|size|图形骨架的大小|`'small' \| 'medium' \| 'large'`|`'medium'`|
