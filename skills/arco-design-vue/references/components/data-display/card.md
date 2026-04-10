---
name: arco-vue-card
description: "Arco Design Vue 卡片 Card 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-card>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 卡片 Card

来源组件：上游 `web-vue/components/card`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-card>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
常规的内容容器，可承载文字、列表、图片、段落，常用于模块划分和内容概览。




```vue
<template>
  <div :style="{ display: 'flex' }">
    <a-card :style="{ width: '360px' }" title="Arco Card">
      <template #extra>
        <a-link>More</a-link>
      </template>
      ByteDance's core product, Toutiao ("Headlines"), is a content platform in
      China and around the world. Toutiao started out as a news recommendation
      engine and gradually evolved into a platform delivering content in various
      formats.
    </a-card>
  </div>
</template>
```

## 示例：鼠标悬浮样式

### 说明
指定 `hoverable` 来为卡片添加鼠标悬浮样式，同时你可以通过样式覆盖来自定义悬浮样式。




```vue
<template>
  <div :style="{ display: 'flex' }">
    <a-card :style="{ width: '360px' }" title="Arco Card" hoverable>
      <template #extra>
        <a-link>More</a-link>
      </template>
      Card content <br />
      Card content
    </a-card>
    <a-card
      class="card-demo"
      title="Custom hover style"
      hoverable
    >
      <template #extra>
        <a-link>More</a-link>
      </template>
      Card content <br />
      Card content
    </a-card>
  </div>
</template>
<style scoped>
.card-demo {
  width: 360px;
  margin-left: 24px;
  transition-property: all;
}
.card-demo:hover {
  transform: translateY(-4px);
}
</style>
```

## 示例：无边框卡片

### 说明
设置 `bordered` 为 `false` 来使用无边框卡片。




```vue
<template>
  <div
    :style="{
      display: 'flex',
      width: '100%',
      boxSizing: 'border-box',
      padding: '40px',
      backgroundColor: 'var(--color-fill-2)',
    }"
  >
    <a-card :style="{ width: '360px' }" title="Arco Card" :bordered="false">
      <template #extra>
        <a-link>More</a-link>
      </template>
      Card content
      <br />
      Card content
    </a-card>
    <a-card
      :style="{ width: '360px', marginLeft: '24px' }"
      title="Hover me"
      hoverable
      :bordered="false"
    >
      <template #extra>
        <a-link>More</a-link>
      </template>
      Card content
      <br />
      Card content
    </a-card>
  </div>
</template>
```

## 示例：简洁卡片

### 说明
卡片可以只有内容区域。




```vue
<template>
  <a-card hoverable :style="{ width: '360px', marginBottom: '20px' }">
    <div
      :style="{
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'space-between',
      }"
    >
      <span
        :style="{ display: 'flex', alignItems: 'center', color: '#1D2129' }"
      >
        <a-avatar
          :style="{ marginRight: '8px', backgroundColor: '#165DFF' }"
          :size="28"
        >
          A
        </a-avatar>
        <a-typography-text>Username</a-typography-text>
      </span>
      <a-link>More</a-link>
    </div>
  </a-card>
</template>
```

## 示例：更灵活的内容展示

### 说明
使用 `Card.Meta` 支持更加灵活的内容（封面、头像、 标题、描述信息）




```vue
<template>
  <a-card hoverable :style="{ width: '360px' }">
    <template #cover>
      <div
        :style="{
          height: '204px',
          overflow: 'hidden',
        }"
      >
        <img
          :style="{ width: '100%', transform: 'translateY(-20px)' }"
          alt="dessert"
          src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a20012a2d4d5b9db43dfc6a01fe508c0.png~tplv-uwbnlip3yd-webp.webp"
        />
      </div>
    </template>
    <a-card-meta title="Card Title">
      <template #description>
        Card content <br />
        Card content
      </template>
    </a-card-meta>
  </a-card>
</template>
```

## 示例：栅格卡片

### 说明
在系统概览页面常常和栅格进行配合。




```vue
<template>
  <div
    :style="{
      boxSizing: 'border-box',
      width: '100%',
      padding: '40px',
      backgroundColor: 'var(--color-fill-2)',
    }"
  >
    <a-row :gutter="20" :style="{ marginBottom: '20px' }">
      <a-col :span="8">
        <a-card title="Arco Card" :bordered="false" :style="{ width: '100%' }">
          <template #extra>
            <a-link>More</a-link>
          </template>
          Card content
        </a-card>
      </a-col>
      <a-col :span="8">
        <a-card title="Arco Card" :bordered="false" :style="{ width: '100%' }">
          <template #extra>
            <a-link>More</a-link>
          </template>
          Card content
        </a-card>
      </a-col>
      <a-col :span="8">
        <a-card title="Arco Card" :bordered="false" :style="{ width: '100%' }">
          <template #extra>
            <a-link>More</a-link>
          </template>
          Card content
        </a-card>
      </a-col>
    </a-row>
    <a-row :gutter="20">
      <a-col :span="16">
        <a-card title="Arco Card" :bordered="false" :style="{ width: '100%' }">
          <template #extra>
            <a-link>More</a-link>
          </template>
          Card content
        </a-card>
      </a-col>
      <a-col :span="8">
        <a-card title="Arco Card" :bordered="false" :style="{ width: '100%' }">
          <template #extra>
            <a-link>More</a-link>
          </template>
          Card content
        </a-card>
      </a-col>
    </a-row>
  </div>
</template>
```

## 示例：网络型内嵌卡片

### 说明
通过 `Card.Grid` 来使用卡片内容区隔模式。




```vue
<template>
  <a-card :bordered="false" :style="{ width: '100%' }">
    <a-card-grid
      v-for="(_, index) in new Array(7)"
      :key="index"
      :hoverable="index % 2 === 0"
      :style="{ width: '25%' }"
    >
      <a-card
        class="card-demo"
        title="Arco Card"
        :bordered="false"
      >
        <template #extra>
          <a-link>More</a-link>
        </template>
        <p :style="{ margin: 0 }">
          {{ index % 2 === 0 ? 'Card allow to hover' : 'Card content' }}
        </p>
      </a-card>
    </a-card-grid>
  </a-card>
</template>
<style scoped>
.card-demo {
  width: 100%;
}
.card-demo :deep(.arco-card-header) {
  border: none;
}
</style>
```

## 示例：内部卡片

### 说明
卡片中可以嵌套其他卡片组件。




```vue
<template>
  <a-card title="Arco Card">
    <a-card :style="{ marginBottom: '20px' }" title="Inner Card Title">
      <template #extra>
        <a-link>More</a-link>
      </template>
      Inner Card Content
    </a-card>
    <a-card title="Inner Card Title">
      <template #extra>
        <a-link>More</a-link>
      </template>
      Inner Card Content
    </a-card>
  </a-card>
</template>
```

## 示例：支持更多内容配置

### 说明
`actions` slot 可以用于展示底部按钮组。




```vue
<template>
  <a-card :style="{ width: '360px' }">
    <template #actions>
      <span class="icon-hover"> <IconThumbUp /> </span>
      <span class="icon-hover"> <IconShareInternal /> </span>
      <span class="icon-hover"> <IconMore /> </span>
    </template>
    <template #cover>
      <div
        :style="{
          height: '204px',
          overflow: 'hidden',
        }"
      >
        <img
          :style="{ width: '100%', transform: 'translateY(-20px)' }"
          alt="dessert"
          src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a20012a2d4d5b9db43dfc6a01fe508c0.png~tplv-uwbnlip3yd-webp.webp"
        />
      </div>
    </template>
    <a-card-meta title="Card Title" description="This is the description">
      <template #avatar>
        <div
          :style="{ display: 'flex', alignItems: 'center', color: '#1D2129' }"
        >
          <a-avatar :size="24" :style="{ marginRight: '8px' }">
            A
          </a-avatar>
          <a-typography-text>Username</a-typography-text>
        </div>
      </template>
    </a-card-meta>
  </a-card>
</template>

<script>
import {
  IconThumbUp,
  IconShareInternal,
  IconMore,
} from '@arco-design/web-vue/es/icon';

export default {
  components: { IconThumbUp, IconShareInternal, IconMore },
};
</script>
<style scoped>
.icon-hover {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  transition: all 0.1s;
}
.icon-hover:hover {
  background-color: rgb(var(--gray-2));
}
</style>
```

## API


### `<card>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|bordered|是否有边框|`boolean`|`true`|
|loading|是否为加载中|`boolean`|`false`|
|hoverable|是否可悬浮|`boolean`|`false`|
|size|卡片尺寸|`'medium' \| 'small'`|`'medium'`|
|header-style|自定义标题区域样式|`CSSProperties`|`() => ({})`|
|body-style|内容区域自定义样式|`CSSProperties`|`() => ({})`|
|title|卡片标题|`string`|`-`|
|extra|卡片右上角的操作区域|`string`|`-`|
### `<card>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|actions|卡片底部的操作组|-|
|cover|卡片封面|-|
|extra|卡片右上角的操作区域|-|
|title|卡片标题|-|




### `<card-meta>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|title|标题|`string`|`-`|
|description|描述|`string`|`-`|
### `<card-meta>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|description|描述|-|
|title|标题|-|
|avatar|头像|-|




### `<card-grid>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|hoverable|是否可以悬浮|`boolean`|`false`|
