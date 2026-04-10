---
name: arco-vue-popconfirm
description: "Arco Design Vue 气泡确认框 Popconfirm 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-popconfirm>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 气泡确认框 Popconfirm

来源组件：上游 `web-vue/components/popconfirm`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-popconfirm>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
气泡确认框的基本用法。




```vue
<template>
  <a-popconfirm content="Are you sure you want to delete?">
    <a-button>Click To Delete</a-button>
  </a-popconfirm>
</template>
```

## 示例：自定义按钮

### 说明
自定义按钮的文字或图标。




```vue
<template>
  <a-popconfirm content="Do you want to discard the draft?" okText="Discard" cancelText="No">
    <a-button>Discard</a-button>
  </a-popconfirm>
</template>
```

## 示例：弹出位置

### 说明
`popconfirm` 支持 12 个不同的方位。分别为：`上左` `上` `上右` `下左` `下` `下右` `左上` `左` `左下` `右上` `右` `右下`。




```vue
<template>
  <div :style="{position: 'relative', width: '440px', height: '280px'}">
    <a-popconfirm content="This is a Popconfirm" position="tl">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'70px'}">TL</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="top">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'180px'}">TOP</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="tr">
      <a-button class="button" :style="{position: 'absolute',top:'0',left:'290px'}">TR</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="bl">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'70px'}">BL</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="bottom">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'180px'}">BOTTOM</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="br">
      <a-button class="button" :style="{position: 'absolute',top:'240px',left:'290px'}">BR</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="lt">
      <a-button class="button" :style="{position: 'absolute',top:'60px',left:'10px'}">LT</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="left">
      <a-button class="button" :style="{position: 'absolute',top:'120px',left:'10px'}">LEFT</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="lb">
      <a-button class="button" :style="{position: 'absolute',top:'180px',left:'10px'}">LB</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="rt">
      <a-button class="button" :style="{position: 'absolute',top:'60px',left:'350px'}">RT</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="right">
      <a-button class="button" :style="{position: 'absolute',top:'120px',left:'350px'}">RIGHT</a-button>
    </a-popconfirm>
    <a-popconfirm content="This is a Popconfirm" position="rb">
      <a-button class="button" :style="{position: 'absolute',top:'180px',left:'350px'}">RB</a-button>
    </a-popconfirm>
  </div>
</template>

<style scoped lang="less">
.button{
  width: 100px;
}
</style>
```

## 示例：确认框类型

### 说明
通过 `type` 属性可以设置确认框类型。




```vue
<template>
  <a-space>
    <a-popconfirm content="Are you sure you want to delete?" type="info">
      <a-button>Click To Delete</a-button>
    </a-popconfirm>
    <a-popconfirm content="Are you sure you want to delete?" type="success">
      <a-button>Click To Delete</a-button>
    </a-popconfirm>
    <a-popconfirm content="Are you sure you want to delete?" type="warning">
      <a-button>Click To Delete</a-button>
    </a-popconfirm>
    <a-popconfirm content="Are you sure you want to delete?" type="error">
      <a-button>Click To Delete</a-button>
    </a-popconfirm>
  </a-space>
</template>
```

`<popconfirm>` 组件继承 `<trigger>` 组件的全部属性

## API


### `<popconfirm>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|content|内容|`string`|`-`|
|position|弹出位置|`'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'`|`'top'`|
|popup-visible **(v-model)**|气泡确认框是否可见|`boolean`|`-`|
|default-popup-visible|气泡确认框默认是否可见（非受控模式）|`boolean`|`false`|
|type|气泡确认框的类型|`'info' \| 'success' \| 'warning' \| 'error'`|`'info'`|
|ok-text|确认按钮的内容|`string`|`-`|
|cancel-text|取消按钮的内容|`string`|`-`|
|ok-loading|确认按钮是否为加载中状态|`boolean`|`false`|
|ok-button-props|确认按钮的Props|`ButtonProps`|`-`|
|cancel-button-props|取消按钮的Props|`ButtonProps`|`-`|
|content-class|弹出框内容的类名|`ClassName`|`-`|
|content-style|弹出框内容的样式|`CSSProperties`|`-`|
|arrow-class|弹出框箭头的类名|`ClassName`|`-`|
|arrow-style|弹出框箭头的样式|`CSSProperties`|`-`|
|popup-container|弹出框的挂载点|`string \| HTMLElement`|`-`|
|on-before-ok|触发 ok 事件前的回调函数。如果返回 false 则不会触发后续事件，也可使用 done 进行异步关闭。|`(  done: (closed: boolean) => void) => void \| boolean \| Promise<void \| boolean>`|`-`|
|on-before-cancel|触发 cancel 事件前的回调函数。如果返回 false 则不会触发后续事件。|`() => boolean`|`-`|
### `<popconfirm>` 事件

|事件名|描述|参数|
|---|---|---|
|popup-visible-change|气泡确认框的显隐状态改变时触发|visible: `boolean`|
|ok|点击确认按钮时触发|-|
|cancel|点击取消按钮时触发|-|
### `<popconfirm>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|icon|图标|-|
|content|内容|-|
