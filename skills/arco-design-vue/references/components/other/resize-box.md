---
name: arco-vue-resize-box
description: "Arco Design Vue 伸缩框 ResizeBox 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-resize-box>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 伸缩框 ResizeBox

来源组件：上游 `web-vue/components/resize-box`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-resize-box>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
`ResizeBox` 伸缩框组件的基础使用。通过设置 `directions`，可以指定四条边中的哪几条边可以进行伸缩。




```vue
<template>
  <div>
    <a-resize-box
      :directions="['right', 'bottom']"
      :style="{ width: '500px', minWidth: '100px', maxWidth: '100%', height: '200px', textAlign: 'center' }"
    >
      <a-typography-paragraph>We are building the future of content discovery and creation.</a-typography-paragraph>
      <a-divider />
      <a-typography-paragraph>
        ByteDance's content platforms enable people to enjoy content powered by AI technology. We
        inform, entertain, and inspire people across language, culture and geography.
      </a-typography-paragraph>
      <a-divider>ByteDance</a-divider>
      <a-typography-paragraph>Yiming Zhang is the founder and CEO of ByteDance.</a-typography-paragraph>
    </a-resize-box>
  </div>
</template>
```

## 示例：受控的高宽

### 说明
`ResizeBox` 的 `width` 和 `height` 都支持 `v-model`。




```vue
<template>
<div>
  <a-resize-box
    :directions="['right', 'bottom']"
    :style="{ minWidth: '100px', maxWidth: '100%', textAlign: 'center' }"
    v-model:width="width"
    v-model:height="height"
  >
    <a-typography-paragraph>We are building the future of content discovery and creation.</a-typography-paragraph>
    <a-divider />
    <a-typography-paragraph>
      ByteDance's content platforms enable people to enjoy content powered by AI technology. We
      inform, entertain, and inspire people across language, culture and geography.
    </a-typography-paragraph>
    <a-divider>ByteDance</a-divider>
    <a-typography-paragraph>Yiming Zhang is the founder and CEO of ByteDance.</a-typography-paragraph>
  </a-resize-box>
</div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const width = ref(500);
    const height = ref(200);
    return {
      width,
      height,
    };
  }
};
</script>
```

## 示例：在布局中使用

### 说明
[Layout](/vue/component/resize-box) 组件中集成了 `ResizeBox` 组件，可以在 Layout 中使用可伸缩的侧边栏。




```vue
<template>
<div class="layout-demo">
  <a-layout>
    <a-layout-header>Header</a-layout-header>
    <a-layout>
      <a-layout-sider :resize-directions="['right']">
        Sider
      </a-layout-sider>
      <a-layout-content>Content</a-layout-content>
    </a-layout>
    <a-layout-footer>Footer</a-layout-footer>
  </a-layout>
</div>
</template>

<style scoped>
.layout-demo :deep(.arco-layout-header),
.layout-demo :deep(.arco-layout-footer),
.layout-demo :deep(.arco-layout-sider-children),
.layout-demo :deep(.arco-layout-content) {
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: var(--color-white);
  font-size: 16px;
  font-stretch: condensed;
  text-align: center;
}


.layout-demo :deep(.arco-layout-header),
.layout-demo :deep(.arco-layout-footer) {
  height: 64px;
  background-color: var(--color-primary-light-4);
}

.layout-demo :deep(.arco-layout-sider) {
  width: 206px;
  background-color: var(--color-primary-light-3);
  min-width: 150px;
  max-width: 500px;
  height: 200px;
}

.layout-demo :deep(.arco-layout-content) {
  background-color: rgb(var(--arcoblue-6));
}
</style>
```

## 示例：定制伸缩杆内容

### 说明
可通过插槽 `resize-trigger` 定制各个方向的伸缩杆的内容。




```vue
<template>
  <a-resize-box
    :directions="['right', 'bottom']"
    style="width: 500px; min-width: 100px; max-width: 100%; height: 200px; text-align: center;"
  >
    <template #resize-trigger="{ direction }">
      <div
        :class="[
          `resizebox-demo`,
          `resizebox-demo-${direction === 'right' ? 'vertical' : 'horizontal'}`
        ]"
      >
        <div class="resizebox-demo-line"/>
      </div>
    </template>
    <a-typography-paragraph>We are building the future of content discovery and creation.</a-typography-paragraph>
    <a-divider />
    <a-typography-paragraph>
      ByteDance's content platforms enable people to enjoy content powered by AI technology. We
      inform, entertain, and inspire people across language, culture and geography.
    </a-typography-paragraph>
    <a-divider>ByteDance</a-divider>
    <a-typography-paragraph>Yiming Zhang is the founder and CEO of ByteDance.</a-typography-paragraph>
  </a-resize-box>
</template>

<style scoped>
  .resizebox-demo {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    background-color: var(--color-bg-2);
  }
  .resizebox-demo::before,
  .resizebox-demo::after {
    width: 6px;
    height: 6px;
    border: 1px solid rgb(var(--arcoblue-6));
    content: '';
}
  .resizebox-demo-line {
    flex: 1;
    background-color: rgb(var(--arcoblue-6));
  }
  .resizebox-demo-vertical {
    flex-direction: column;
  }
  .resizebox-demo-vertical .resizebox-demo-line {
    width: 1px;
    height: 100%;
  }
  .resizebox-demo-horizontal .resizebox-demo-line {
    height: 1px;
  }
</style>
```

## API


### `<resize-box>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|width **(v-model)**|宽度|`number`|`-`|
|height **(v-model)**|高度|`number`|`-`|
|component|伸缩框的 html 标签|`string`|`'div'`|
|directions|可以进行伸缩的边，有上、下、左、右可以使用|`('left' \| 'right' \| 'top' \| 'bottom')[]`|`['right']`|
### `<resize-box>` 事件

|事件名|描述|参数|
|---|---|---|
|moving-start|拖拽开始时触发|ev: `MouseEvent`|
|moving|拖拽时触发|size: `{ width: number; height: number; }`<br>ev: `MouseEvent`|
|moving-end|拖拽结束时触发|ev: `MouseEvent`|
### `<resize-box>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|resize-trigger|伸缩杆的内容|direction: `'left' \| 'right' \| 'top' \| 'bottom'`|
|resize-trigger-icon|伸缩杆的图标|direction: `'left' \| 'right' \| 'top' \| 'bottom'`|
