---
name: arco-vue-popover
description: "Arco Design Vue 气泡卡片 Popover 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-popover>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 气泡卡片 Popover

来源组件：上游 `web-vue/components/popover`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-popover>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
鼠标移入或点击，弹出气泡，可对浮层上元素进行操作，承载复杂内容和操作。




```vue
<template>
  <a-popover title="Title">
    <a-button>Hover</a-button>
    <template #content>
      <p>Here is the text content</p>
      <p>Here is the text content</p>
    </template>
  </a-popover>
</template>
```

## 示例：触发方式

### 说明
通过设置 `trigger`，可以指定不同的触发方式。




```vue
<template>
  <a-space>
    <a-popover title="Title">
      <a-button>Hover Me</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover title="Title" trigger="click">
      <a-button>Click Me</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
  </a-space>
</template>
```

## 示例：弹出位置

### 说明
`Popover`支持 12 个不同的方位。分别为：`上左` `上` `上右` `下左` `下` `下右` `左上` `左` `左下` `右上` `右` `右下`。




```vue
<template>
  <div :style="{position: 'relative', width: '440px', height: '280px'}">
    <a-popover position="tl">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'70px'}">TL</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="top">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'180px'}">TOP</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="tr">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'290px'}">TR</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="bl">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'70px'}">BL</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="bottom">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'180px'}">BOTTOM</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="br">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'290px'}">BR</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="lt">
      <a-button class="button" :style="{position: 'absolute',top:'60px',left:'10px'}">LT</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="left">
      <a-button class="button" :style="{position: 'absolute',top:'120px',left:'10px'}">LEFT</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="lb">
      <a-button class="button" :style="{position: 'absolute',top:'180px',left:'10px'}">LB</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="rt">
      <a-button class="button" :style="{position: 'absolute',top:'60px',left:'350px'}">RT</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="right">
      <a-button class="button" :style="{position: 'absolute',top:'120px',left:'350px'}">RIGHT</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-popover position="rb">
      <a-button class="button" :style="{position: 'absolute',top:'180px',left:'350px'}">RB</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
  </div>
</template>

<style scoped lang="less">
.button{
  width: 100px;
}
</style>
```

`<popover>` 组件继承 `<trigger>` 组件的全部属性

## API


### `<popover>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|popup-visible **(v-model)**|文字气泡是否可见|`boolean`|`-`|
|default-popup-visible|文字气泡默认是否可见（非受控模式）|`boolean`|`false`|
|title|标题|`string`|`-`|
|content|内容|`string`|`-`|
|trigger|触发方式|`'hover' \| 'click' \| 'focus' \| 'contextMenu'`|`'hover'`|
|position|弹出位置|`'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'`|`'top'`|
|content-class|弹出框内容的类名|`ClassName`|`-`|
|content-style|弹出框内容的样式|`CSSProperties`|`-`|
|arrow-class|弹出框箭头的类名|`ClassName`|`-`|
|arrow-style|弹出框箭头的样式|`CSSProperties`|`-`|
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`-`|
### `<popover>` 事件

|事件名|描述|参数|
|---|---|---|
|popup-visible-change|文字气泡显示状态改变时触发|visible: `boolean`|
### `<popover>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|title|标题|-|
|content|内容|-|
