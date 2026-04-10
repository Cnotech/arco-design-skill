---
name: arco-vue-alert
description: "Arco Design Vue 警告提示 Alert 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-alert>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 警告提示 Alert

来源组件：上游 `web-vue/components/alert`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-alert>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
展现需要关注的信息，适用于简短的警告提示。




```vue
<template>
  <a-alert>This is an info alert.</a-alert>
</template>
```

## 示例：提示类型

### 说明
警告提示有 `info`、`success`、`warning`、`error` 四种类型。2.41.0 版本新增 `normal` 类型，此类型下默认不展示图标。




```vue
<template>
  <a-row :gutter="[40, 20]">
    <a-col :span="12">
      <a-alert>This is an info alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="success">This is an success alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="warning">This is an warning alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="error">This is an error alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="normal">
        <template #icon>
          <icon-exclamation-circle-fill />
        </template>
        This is an normal alert.
      </a-alert>
    </a-col>
  </a-row>
</template>

<script>
import { IconExclamationCircleFill } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconExclamationCircleFill }
};
</script>
```

## 示例：提示标题

### 说明
通过设置 `title` 可以给警告提示添加标题。




```vue
<template>
  <a-row :gutter="[40, 20]">
    <a-col :span="12">
      <a-alert title="Info">This is an info alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert title="Success" type="success">This is an success alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="warning">
        <template #title>
          Warning
        </template>
        This is an warning alert.
      </a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="error">
        <template #title>
          Error
        </template>
        This is an error alert.
      </a-alert>
    </a-col>
  </a-row>
</template>
```

## 示例：可关闭

### 说明
通过设置 `closable`，可开启关闭按钮。




```vue
<template>
  <a-row :gutter="[40, 20]">
    <a-col :span="12">
      <a-alert closable>This is an info alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="success" closable>This is an success alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="warning" closable>
        <template #title>
          Warning
        </template>
        This is an warning alert.
      </a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="error" closable>
        <template #title>
          Error
        </template>
        This is an error alert.
      </a-alert>
    </a-col>
  </a-row>
</template>
```

## 示例：自定义关闭元素

### 说明
指定 `close-element` slot，自定义关闭元素。




```vue
<template>
  <a-row :gutter="[40, 20]">
    <a-col :span="12">
      <a-alert closable>
        <template #close-element>
          <icon-close-circle />
        </template>
        This is an info alert.
      </a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert closable>
        <template #close-element>
          Close
        </template>
        This is an info alert.
      </a-alert>
    </a-col>
  </a-row>
</template>
```

## 示例：隐藏图标

### 说明
通过设置 `:show-icon="false"` 来隐藏图标。




```vue
<template>
  <a-row :gutter="[40, 20]">
    <a-col :span="12">
      <a-alert :show-icon="false">This is an info alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="success" :show-icon="false">This is an success alert.</a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="warning" :show-icon="false">
        <template #title>
          Warning
        </template>
        This is an warning alert.
      </a-alert>
    </a-col>
    <a-col :span="12">
      <a-alert type="error" :show-icon="false">
        <template #title>
          Error
        </template>
        This is an error alert.
      </a-alert>
    </a-col>
  </a-row>
</template>
```

## 示例：操作项

### 说明
通过 `#action` 插槽自定义操作按钮




```vue
<template>
  <a-space direction="vertical" size="large" style="width: 100%;">
    <a-alert closable>
      This is an info alert.
      <template #action>
        <a-button size="small" type="primary">Detail</a-button>
      </template>
    </a-alert>
    <a-alert title="Example" closable>
      This is an info alert.
      <template #action>
        <a-button size="small" type="primary">Detail</a-button>
      </template>
    </a-alert>
  </a-space>
</template>
```

## 示例：顶部公告

### 说明
通过设置 `banner`，可将警告提示作为顶部公告使用（去除边框和圆角）。




```vue
<template>
  <a-alert banner center>This is an info alert.</a-alert>
</template>
```

## API


### `<alert>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|警告提示的类型。2.41.0 新增 `normal` 类型|`info \| success \| warning \| error \| normal`|`'info'`|
|show-icon|是否展示图标|`boolean`|`true`|
|closable|是否展示关闭按钮|`boolean`|`false`|
|title|警告提示的标题|`string`|`-`|
|banner|是否作为顶部公告使用（去除边框和圆角）|`boolean`|`false`|
|center|内容是否居中显示|`boolean`|`false`|
### `<alert>` 事件

|事件名|描述|参数|
|---|---|---|
|close|点击关闭按钮时触发|ev: `MouseEvent`|
|after-close|关闭动画结束后触发|-|
### `<alert>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|icon|图标|-||
|title|标题|-||
|action|操作项|-||
|close-element|关闭元素|-|2.36.0|
