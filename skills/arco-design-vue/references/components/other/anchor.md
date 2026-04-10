---
name: arco-vue-anchor
description: "Arco Design Vue 锚点 Anchor 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-anchor>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 锚点 Anchor

来源组件：上游 `web-vue/components/anchor`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-anchor>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
锚点的基础用法




```vue
<template>
  <a-anchor>
    <a-anchor-link href="#basic">Basic</a-anchor-link>
    <a-anchor-link href="#line-less">LineLess Mode</a-anchor-link>
    <a-anchor-link href="#affix">
      Affix
      <template #sublist>
        <a-anchor-link href="#boundary">Scroll Boundary</a-anchor-link>
        <a-anchor-link href="#hash">Hash mode</a-anchor-link>
      </template>
    </a-anchor-link>
  </a-anchor>
</template>
```

## 示例：无轴线模式

### 说明
设置 `line-less` 时，可以使用无左侧轴线的锚点样式。




```vue
<template>
  <a-anchor line-less>
    <a-anchor-link href="#basic">Basic</a-anchor-link>
    <a-anchor-link href="#line-less">LineLess Mode</a-anchor-link>
    <a-anchor-link href="#affix">
      Affix
      <template #sublist>
        <a-anchor-link href="#boundary">Scroll Boundary</a-anchor-link>
        <a-anchor-link href="#hash">Hash mode</a-anchor-link>
      </template>
    </a-anchor-link>
  </a-anchor>
</template>
```

## 示例：固钉位置

### 说明
使用 `affix` 组件可以让锚点固定在页面之内。




```vue
<template>
  <a-affix :offsetTop="80">
    <a-anchor :style="{backgroundColor: 'var(--color-bg-1)'}">
      <a-anchor-link href="#basic">Basic</a-anchor-link>
      <a-anchor-link href="#line-less">LineLess Mode</a-anchor-link>
      <a-anchor-link href="#affix">
        Affix
        <template #sublist>
          <a-anchor-link href="#boundary">Scroll Boundary</a-anchor-link>
          <a-anchor-link href="#hash">Hash mode</a-anchor-link>
        </template>
      </a-anchor-link>
    </a-anchor>
  </a-affix>
</template>
```

## 示例：锚点滚动偏移量

### 说明
可以设置 `boundary` 来定制锚点滚动偏移量。




```vue
<template>
  <a-anchor boundary="center">
    <a-anchor-link href="#basic">Basic</a-anchor-link>
    <a-anchor-link href="#line-less">LineLess Mode</a-anchor-link>
    <a-anchor-link href="#affix">
      Affix
      <template #sublist>
        <a-anchor-link href="#boundary">Scroll Boundary</a-anchor-link>
        <a-anchor-link href="#hash">Hash mode</a-anchor-link>
      </template>
    </a-anchor-link>
  </a-anchor>
</template>
```

## 示例：是否改变hash

### 说明
可以设置点击锚点而不改变浏览器历史。




```vue
<template>
  <a-anchor :change-hash="false">
    <a-anchor-link href="#basic">Basic</a-anchor-link>
    <a-anchor-link href="#line-less">LineLess Mode</a-anchor-link>
    <a-anchor-link href="#affix">
      Affix
      <template #sublist>
        <a-anchor-link href="#boundary">Scroll Boundary</a-anchor-link>
        <a-anchor-link href="#hash">Hash mode</a-anchor-link>
      </template>
    </a-anchor-link>
  </a-anchor>
</template>
```

## API


### `<anchor>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|boundary|滚动边界值，设置该值为数字后，将会在距离滚动容器 `boundary` 距离时停止滚动。|`'start' \| 'end' \| 'center' \| 'nearest' \| number`|`'start'`|
|line-less|是否显示左侧轴线|`boolean`|`false`|
|scroll-container|滚动容器|`string \| HTMLElement \| Window`|`-`|
|change-hash|是否改变hash。设置为 `false` 时点击锚点不会改变页面的 hash|`boolean`|`true`|
|smooth|是否使用平滑滚动|`boolean`|`true`|
### `<anchor>` 事件

|事件名|描述|参数|
|---|---|---|
|select|用户点击链接时触发|hash: ` string \| undefined `<br>preHash: `string`|
|change|链接发生改变时触发|hash: `string`|




### `<anchor-link>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|title|锚点链接的文本内容|`string`|`-`|
|href|锚点链接的地址|`string`|`-`|
