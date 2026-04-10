---
name: arco-vue-typography
description: "Arco Design Vue 排版 Typography 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-typography>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 排版 Typography

来源组件：上游 `web-vue/components/typography`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-typography>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：组合使用

### 说明
排版组件用于展示标题、段落、文本内容，这里展示了排版的组合使用。




```vue
<template>
  <a-typography :style="{ marginTop: '-40px' }">
    <a-typography-title>
      Design system
    </a-typography-title>
    <a-typography-paragraph>
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design.
    </a-typography-paragraph>
    <a-typography-paragraph>
      In some cases, the direct construction of an object without an explicit prior plan (such as in craftwork, some engineering, coding, and graphic design) may also be considered <a-typography-text bold>to be a design activity.</a-typography-text>
    </a-typography-paragraph>
    <a-typography-title :heading="2">ArcoDesign</a-typography-title>
    <a-typography-paragraph>
      The ArcoDesign component library defines a set of default particle variables, and a custom theme is to <a-typography-text mark>customize</a-typography-text> and <a-typography-text underline>overwrite</a-typography-text> this variable list.
    </a-typography-paragraph>
    <a-typography-paragraph blockquote>
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a <a-typography-text code>prototype</a-typography-text>, <a-typography-text code>product</a-typography-text> or <a-typography-text code>process</a-typography-text>. The verb to design expresses the process of developing a design.
    </a-typography-paragraph>
    <a-typography-paragraph mark underline delete>A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process.</a-typography-paragraph>
    <a-typography-paragraph>
      <ul>
        <li>
          Architectural blueprints
          <ul>
            <li>Architectural blueprints</li>
          </ul>
        </li>
        <li>Engineering drawings</li>
        <li>Business processes</li>
      </ul>
    </a-typography-paragraph>
    <a-typography-paragraph>
      <ol>
        <li>Architectural blueprints</li>
        <li>Engineering drawings</li>
        <li>Business processes</li>
      </ol>
    </a-typography-paragraph>
  </a-typography>
</template>
```

## 示例：标题

### 说明
展示不同级别的标题。




```vue
<template>
  <a-typography>
    <a-typography-title>
      H1. The Pragmatic Romanticism
    </a-typography-title>
    <a-typography-title :heading="2">
      H2. The Pragmatic Romanticism
    </a-typography-title>
    <a-typography-title :heading="3">
      H3. The Pragmatic Romanticism
    </a-typography-title>
    <a-typography-title :heading="4">
      H4. The Pragmatic Romanticism
    </a-typography-title>
    <a-typography-title :heading="5">
      H5. The Pragmatic Romanticism
    </a-typography-title>
    <a-typography-title :heading="6">
      H6. The Pragmatic Romanticism
    </a-typography-title>
  </a-typography>
</template>
```

## 示例：文本

### 说明
不同样式的文本以及超链接组件。




```vue
<template>
<a-space direction="vertical" :size="10">
    <a-typography-text>
      Arco Design
    </a-typography-text>
    <a-typography-text type="secondary">
      Secondary
    </a-typography-text>
    <a-typography-text type="primary">
      Primary
    </a-typography-text>
    <a-typography-text type="success">
      Success
    </a-typography-text>
    <a-typography-text type="warning">
      Warning
    </a-typography-text>
    <a-typography-text type="danger">
      Danger
    </a-typography-text>
    <a-typography-text bold>
      Bold
    </a-typography-text>
    <a-typography-text disabled>
      Disabled
    </a-typography-text>
    <a-typography-text mark>
      Mark
    </a-typography-text>
    <a-typography-text underline>
      Underline
    </a-typography-text>
    <a-typography-text delete>
      Line through
    </a-typography-text>
    <a-typography-text code>
      Code snippet
    </a-typography-text>
  </a-space>
</template>
```

## 示例：段落

### 说明
文本段落样式。




```vue
<template>
  <a-typography>
    <a-typography-title :heading="5">Default</a-typography-title>
    <a-typography-paragraph>
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. In some cases, the direct construction of an object without an explicit prior plan (such as in craftwork, some engineering, coding, and graphic design) may also be considered to be a design activity.
    </a-typography-paragraph>
    <a-typography-title :heading="5">Secondary</a-typography-title>
    <a-typography-paragraph type="secondary">
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. In some cases, the direct construction of an object without an explicit prior plan (such as in craftwork, some engineering, coding, and graphic design) may also be considered to be a design activity.
    </a-typography-paragraph>
    <a-typography-title :heading="5">Spacing default</a-typography-title>
    <a-typography-paragraph>
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. In some cases, the direct construction of an object without an explicit prior plan (such as in craftwork, some engineering, coding, and graphic design) may also be considered to be a design activity.
    </a-typography-paragraph>
    <a-typography-title :heading="5">Spacing close</a-typography-title>
    <a-typography-paragraph type="secondary" spacing="close">
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design.
    </a-typography-paragraph>
  </a-typography>
</template>
```

## 示例：可交互

### 说明
提供复制、编辑文本等功能。




```vue
<template>
  <a-typography>
    <a-typography-paragraph copyable>
      Click the icon to copy this text.
    </a-typography-paragraph>
    <a-typography-paragraph
      editable
      v-model:editText="str"
    >
      {{str}}
    </a-typography-paragraph>
  </a-typography>
</template>
<script>
import { defineComponent, ref } from 'vue';
export default defineComponent({
  setup() {
    const str = ref('Click the icon to edit this text.');
    return {
      str,
    }
  }
});
</script>
```

## 示例：省略

### 说明
在空间不足时省略多行文本内容。




```vue
<template>
  <div>
    <a-typography-title :heading="4" ellipsis>
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process.
    </a-typography-title>
    <a-typography-paragraph
      :ellipsis="{
        rows: 2,
        showTooltip: true,
      }"
    >
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. The verb to design expresses the process of developing a design.A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. The verb to design expresses the process of developing a design.
    </a-typography-paragraph>
    <a-typography-paragraph
      :ellipsis="{
        rows: 2,
        showTooltip: true,
        css: true
      }"
    >
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. The verb to design expresses the process of developing a design.A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. The verb to design expresses the process of developing a design.
    </a-typography-paragraph>
    <a-typography-paragraph
      :ellipsis="{
        suffix: '--Arco Design',
        rows: 2,
        expandable: true,
        showTooltip: {
          type: 'popover',
          props: {
            style: { maxWidth: `500px` }
          }
        },
      }"
    >
      <template #expand-node="{expanded}">
        {{ expanded ? '' : 'More' }}
      </template>
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. The verb to design expresses the process of developing a design.A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. The verb to design expresses the process of developing a design.
    </a-typography-paragraph>
    <a-typography-paragraph
      :ellipsis="{
        suffix: '--Arco Design',
        rows: 3,
        expandable: true,
      }"
    >
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. The verb to design expresses the process of developing a design.
      A design is a plan or specification for the construction of an object or system or for the implementation of an activity or process, or the result of that plan or specification in the form of a prototype, product or process. The verb to design expresses the process of developing a design. The verb to design expresses the process of developing a design.
    </a-typography-paragraph>
  </div>
</template>
```

## API






### `Common` Props

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|type|文本类型|`'primary' \| 'secondary' \| 'success' \| 'danger' \| 'warning'`|`-`||
|bold|粗体|`boolean`|`false`||
|mark|添加标记样式|`boolean \| { color: string }`|`false`||
|underline|下划线样式|`boolean`|`false`||
|delete|删除线样式|`boolean`|`false`||
|code|代码块样式|`boolean`|`false`||
|disabled|禁用状态|`boolean`|`false`||
|editable|开启可编辑功能|`boolean`|`false`||
|editing **(v-model)**|是否在编辑状态|`boolean`|`-`||
|default-editing|默认的编辑状态|`boolean`|`false`||
|edit-text **(v-model)**|编辑的文字|`string`|`-`||
|copyable|开启复制功能|`boolean`|`false`||
|copy-text|复制的文字|`string`|`-`||
|copy-delay|复制成功后，复制按钮恢复到可点击状态的延迟时间，单位是毫秒|`number`|`3000`|2.16.0|
|ellipsis|自动溢出省略，具体参数配置看 [EllipsisConfig](#EllipsisConfig)|`boolean \| EllipsisConfig`|`false`||
|edit-tooltip-props|编辑按钮问题提示配置|`object`|`-`|2.32.0|
|copy-tooltip-props|拷贝按钮问题提示配置|`object`|`-`|2.32.0|
### `Common` Events

|事件名|描述|参数|
|---|---|---|
|edit-start|开始编辑|-|
|change|编辑内容变化|text: `string`|
|edit-end|编辑结束|-|
|copy|复制|text: `string`|
|ellipsis|省略变化事件|isEllipsis: `boolean`|
|expand|展开收起事件|expanded: `boolean`|
### `Common` Slots

|插槽名|描述|参数|
|---|:---:|---|
|expand-node|自定义展开和折叠按钮|expanded: `boolean`|
|copy-icon|自定义复制按钮图标|copied: `boolean`|
|copy-tooltip|自定义复制按钮的 tooltip 内容|copied: `boolean`|




### `<typography-title>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|heading|标题级别，相当于 `h1` `h2` `h3` `h4` `h5` `h6`|`'1' \| '2' \| '3' \| '4' \| '5' \| '6'`|`1`|




### `<typography-paragraph>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|blockquote|长引用|`boolean`|`false`|
|spacing|段落的的行高，长文本(大于5行)的时候推荐使用默认行高，短文本(小于等于3行)推荐使用 `close` 紧密的行高。|`'default' \| 'close'`|`'default'`|








### EllipsisConfig

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|rows|显示省略的行数|`number`|`1`||
|expandable|是否支持展开/折叠|`boolean`|`false`||
|ellipsisStr|省略号|`string`|`'...'`||
|suffix|后缀|`string`|`-`||
|showTooltip|配置省略时的弹出框|`boolean    \| { type: 'tooltip' \| 'popover'; props: Record<string, any> }`|`false`||
|css|是否使用 CSS 省略（此模式暂不支持展开、自定义省略号和后缀）|`boolean`|`false`|2.37.0|
