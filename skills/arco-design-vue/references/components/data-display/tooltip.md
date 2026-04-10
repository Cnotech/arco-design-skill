---
name: arco-vue-tooltip
description: "Arco Design Vue 文字气泡 Tooltip 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-tooltip>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 文字气泡 Tooltip

来源组件：上游 `web-vue/components/tooltip`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-tooltip>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
鼠标移入，气泡出现，鼠标移出，气泡消失。




```vue
<template>
  <a-space>
    <a-tooltip content="This is tooltip content">
      <a-button>Mouse over to display tooltip</a-button>
    </a-tooltip>
    <a-tooltip content="This is a two-line tooltip content.This is a two-line tooltip content.">
      <a-button>Mouse over to display tooltip</a-button>
    </a-tooltip>
  </a-space>
</template>
```

## 示例：迷你尺寸

### 说明
适用于小场景或数字气泡样式。




```vue
<template>
  <a-tooltip content="1234" position="top" mini>
    <a-button>Mouse over to display tooltip</a-button>
  </a-tooltip>
</template>
```

## 示例：位置

### 说明
文字气泡支持 12 个不同的方位。分别为：`上左`、`上`、`上右`、`下左`、`下`、`下右`、`左上`、`左`、`左下`、`右上`、`右`、`右下`。




```vue
<template>
  <div :style="{position: 'relative', width: '440px', height: '280px'}">
    <a-tooltip content="This is a Tooltip" position="tl">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'70px'}">TL</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="top">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'180px'}">TOP</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="tr">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'290px'}">TR</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="bl">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'70px'}">BL</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="bottom">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'180px'}">BOTTOM</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="br">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'290px'}">BR</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="lt">
      <a-button class="button" :style="{position: 'absolute',top:'60px',left:'10px'}">LT</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="left">
      <a-button class="button" :style="{position: 'absolute',top:'120px',left:'10px'}">LEFT</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="lb">
      <a-button class="button" :style="{position: 'absolute',top:'180px',left:'10px'}">LB</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="rt">
      <a-button class="button" :style="{position: 'absolute',top:'60px',left:'350px'}">RT</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="right">
      <a-button class="button" :style="{position: 'absolute',top:'120px',left:'350px'}">RIGHT</a-button>
    </a-tooltip>
    <a-tooltip content="This is a Tooltip" position="rb">
      <a-button class="button" :style="{position: 'absolute',top:'180px',left:'350px'}">RB</a-button>
    </a-tooltip>
  </div>
</template>

<style scoped>
.button {
  width: 100px;
}
</style>
```

## 示例：自定义背景颜色

### 说明
通过 `background-color` 属性自定义背景颜色。




```vue
<template>
  <a-space>
    <a-tooltip content="This is tooltip content" background-color="#3491FA">
      <a-button>#3491FA</a-button>
    </a-tooltip>
    <a-tooltip content="This is tooltip content" background-color="#165DFF">
      <a-button>#165DFF</a-button>
    </a-tooltip>
    <a-tooltip content="This is tooltip content" background-color="#722ED1">
      <a-button>#722ED1</a-button>
    </a-tooltip>
  </a-space>
</template>
```

`<tooltip>` 组件继承 `<trigger>` 组件的全部属性

## API


### `<tooltip>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|popup-visible **(v-model)**|文字气泡是否可见|`boolean`|`-`|
|default-popup-visible|文字气泡默认是否可见（非受控模式）|`boolean`|`false`|
|disabled|文字气泡是否禁用|`boolean`|`false`|
|content|文字气泡内容|`string`|`-`|
|position|弹出位置|`'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'`|`'top'`|
|mini|是否展示为迷你尺寸|`boolean`|`false`|
|background-color|弹出框的背景颜色|`string`|`-`|
|content-class|弹出框内容的类名|`ClassName`|`-`|
|content-style|弹出框内容的样式|`CSSProperties`|`-`|
|arrow-class|弹出框箭头的类名|`ClassName`|`-`|
|arrow-style|弹出框箭头的样式|`CSSProperties`|`-`|
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`-`|
### `<tooltip>` 事件

|事件名|描述|参数|
|---|---|---|
|popup-visible-change|文字气泡显示状态改变时触发|visible: `boolean`|
### `<tooltip>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|content|内容|-|
