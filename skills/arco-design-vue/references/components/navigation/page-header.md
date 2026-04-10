---
name: arco-vue-page-header
description: "Arco Design Vue 页头 PageHeader 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-page-header>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 页头 PageHeader

来源组件：上游 `web-vue/components/page-header`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-page-header>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
基础页头，适合使用在需要简单描述的场景。默认是没有底色的。




```vue
<template>
  <div :style="{ background: 'var(--color-fill-2)', padding: '28px' }" >
    <a-page-header
      :style="{ background: 'var(--color-bg-2)' }"
      title="ArcoDesign"
      subtitle="ArcoDesign Vue 2.0"
    >
      <template #extra>
        <a-radio-group type="button" default-value="large">
          <a-radio value="mini">Mini</a-radio>
          <a-radio value="small">Small</a-radio>
          <a-radio value="large">Large</a-radio>
        </a-radio-group>
      </template>
    </a-page-header>
  </div>
</template>
```

## 示例：带有面包屑

### 说明
在页头中展示面包屑。




```vue
<template>
  <div :style="{ background: 'var(--color-fill-2)', padding: '28px' }" >
    <a-page-header
      :style="{ background: 'var(--color-bg-2)' }"
      title="ArcoDesign"
      subtitle="ArcoDesign Vue 2.0"
      :show-back="false"
    >
      <template #breadcrumb>
        <a-breadcrumb>
          <a-breadcrumb-item>Home</a-breadcrumb-item>
          <a-breadcrumb-item>Channel</a-breadcrumb-item>
          <a-breadcrumb-item>News</a-breadcrumb-item>
        </a-breadcrumb>
      </template>
      <template #extra>
        <a-radio-group type="button" default-value="large">
          <a-radio value="mini">Mini</a-radio>
          <a-radio value="small">Small</a-radio>
          <a-radio value="large">Large</a-radio>
        </a-radio-group>
      </template>
    </a-page-header>
  </div>
</template>

```

## 示例：透明底色

### 说明
默认是没有底色的，如果有需要可以通过`style`或类名设置不同底色。




```vue
<template>
  <div :style="{
    backgroundImage: 'radial-gradient(var(--color-fill-3) 1px, rgba(0, 0, 0, 0) 1px)',
    backgroundSize: '16px 16px',
    padding: '28px',
  }">
    <a-page-header title="ArcoDesign" subtitle="ArcoDesign Vue 2.0">
      <template #breadcrumb>
        <a-breadcrumb>
          <a-breadcrumb-item>Home</a-breadcrumb-item>
          <a-breadcrumb-item>Channel</a-breadcrumb-item>
          <a-breadcrumb-item>News</a-breadcrumb-item>
        </a-breadcrumb>
      </template>
      <template #extra>
        <a-radio-group type="button">
          <a-radio value="mini">Mini</a-radio>
          <a-radio value="small">Small</a-radio>
          <a-radio value="large">Large</a-radio>
        </a-radio-group>
      </template>
    </a-page-header>
  </div>
</template>
```

## 示例：组合示例

### 说明
页头的完整示例。




```vue
<template>
  <div :style="{ background: 'var(--color-fill-2)', padding: '28px' }" >
    <a-page-header
      :style="{ background: 'var(--color-bg-2)' }"
      title="ArcoDesign"
    >
      <template #breadcrumb>
        <a-breadcrumb>
          <a-breadcrumb-item>Home</a-breadcrumb-item>
          <a-breadcrumb-item>Channel</a-breadcrumb-item>
          <a-breadcrumb-item>News</a-breadcrumb-item>
        </a-breadcrumb>
      </template>
      <template #subtitle>
        <a-space>
          <span>ArcoDesign Vue 2.0</span>
          <a-tag color="red" size="small">Default</a-tag>
        </a-space>
      </template>
      <template #extra>
        <a-space>
          <a-button>Cancel</a-button>
          <a-button type="primary">Save</a-button>
        </a-space>
      </template>
      <p>
        For other uses, see Design
      </p>
      <p>
        A design is a plan or specification for the construction of an object or system or for the
        implementation of an activity or process, or the result of that plan or specification in the
        form of a prototype, product or process. The verb to design expresses the process of
        developing a design. In some cases, the direct construction of an object without an explicit
        prior plan (such as in craftwork, some engineering, coding, and graphic design) may also be
        considered to be a design activity. The design usually has to satisfy certain goals and
        constraints, may take into account aesthetic, functional, economic, or socio-political
        considerations, and is expected to interact with a certain environment. Major examples of
        designs include architectural blueprints,engineering drawings, business processes, circuit
        diagrams, and sewing patterns.Major examples of designs include architectural
        blueprints,engineering drawings, business processes, circuit diagrams, and sewing patterns.
      </p>
    </a-page-header>
  </div>
</template>

<script>
export default {
}
</script>
```

## API


### `<page-header>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|title|页头的主标题|`string`|`-`|
|subtitle|页头的次标题|`string`|`-`|
|show-back|是否显示返回按钮|`boolean`|`true`|
### `<page-header>` 事件

|事件名|描述|参数|
|---|---|---|
|back|点击返回按钮时触发|event: `Event`|
### `<page-header>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|breadcrumb|面包屑|-||
|back-icon|返回按钮|-|2.36.0|
|title|主标题|-||
|subtitle|次标题|-||
|extra|额外的展示内容|-||
