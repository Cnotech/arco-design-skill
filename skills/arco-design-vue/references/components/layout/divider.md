---
name: arco-vue-divider
description: "Arco Design Vue 分割线 Divider 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-divider>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 分割线 Divider

来源组件：上游 `web-vue/components/divider`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-divider>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
对不同章节的文本段落进行分割，默认为水平分割线，可在中间加入文字。




```vue
<template>
  <div class="divider-demo">
    <p>A design is a plan or specification for the construction of an object.</p>
    <a-divider />
    <p>A design is a plan or specification for the construction of an object.</p>
    <a-divider dashed />
    <p>A design is a plan or specification for the construction of an object.</p>
    <a-divider :size="2" style="border-bottom-style: dotted" />
    <p>A design is a plan or specification for the construction of an object.</p>
  </div>
  <div class="divider-demo" style="marginTop: 48px">
    <div class="flex-box">
      <span class="avatar"><IconImage /></span>
      <div class="content">
        <a-typography-title :heading="6">Image</a-typography-title>
        May 4, 2010
      </div>
    </div>
    <a-divider class="half-divider" />
    <div class="flex-box">
      <span class="avatar"><IconUser /></span>
      <div class="content">
        <a-typography-title :heading="6">Avatar</a-typography-title>
        May 4, 2010
      </div>
    </div>
    <a-divider class="half-divider" />
    <div class="flex-box">
      <span class="avatar"><IconPen /></span>
      <div class="content">
        <a-typography-title :heading="6">Icon</a-typography-title>
        May 4, 2010
      </div>
    </div>
  </div>
</template>

<script>
import {
  IconImage,
  IconUser,
  IconPen,
} from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconImage,
    IconUser,
    IconPen,
  },
};
</script>

<style scoped>
.divider-demo {
  box-sizing: border-box;
  width: 560px;
  padding: 24px;
  border: 30px solid rgb(var(--gray-2));
}
.half-divider {
  left: 55px;
  width: calc(100% - 55px);
  min-width: auto;
  margin: 16px 0;
}
.flex-box {
  display: flex;
  align-items: center;
  justify-content: center;
}
.flex-box .avatar {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  margin-right: 16px;
  color: var(--color-text-2);
  font-size: 16px;
  background-color: var(--color-fill-3);
  border-radius: 50%;
}
.flex-box .content {
  flex: 1;
  color: var(--color-text-2);
  font-size: 12px;
  line-height: 20px;
}
</style>
```

## 示例：带有文字的分割线

### 说明
通过 `orientation` 为分割线添加描述文字。




```vue
<template>
  <div class="divider-demo">
    <p>A design is a plan or specification for the construction of an object.</p>
    <a-divider orientation="left">Text</a-divider>
    <p>A design is a plan or specification for the construction of an object.</p>
    <a-divider orientation="center">Text</a-divider>
    <p>A design is a plan or specification for the construction of an object.</p>
    <a-divider orientation="right">Text</a-divider>
    <a-divider :margin="10"><icon-star /></a-divider>
  </div>
</template>

<style scoped>
.divider-demo {
  box-sizing: border-box;
  width: 560px;
  padding: 24px;
  border: 30px solid rgb(var(--gray-2));
}
</style>
```

## 示例：竖直分割线

### 说明
指定 `direction` 为 `vertical` 即可使用竖直分割线。竖直分割线不能带文字。




```vue
<template>
  <div class="divider-demo">
    <span>Item 1</span>
    <a-divider direction="vertical" />
    <span>Item 2</span>
    <a-divider direction="vertical" />
    <span>Item 3</span>
  </div>
</template>

<style scoped>
.divider-demo {
  box-sizing: border-box;
  width: 560px;
  padding: 24px;
  border: 30px solid rgb(var(--gray-2));
}
</style>
```

## API


### `<divider>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|direction|分割线的方向，是水平还是竖直|`'horizontal' \| 'vertical'`|`'horizontal'`||
|orientation|分割线文字的位置|`'left' \| 'center' \| 'right'`|`'center'`||
|type|分割线样式类型|`'solid' \| 'dashed' \| 'dotted' \| 'double'`|`-`|2.35.0|
|size|分割线宽度/高度|`number`|`-`|2.35.0|
|margin|分割线上下 margin (垂直方向时为左右 margin)|`number \| string`|`-`|2.35.0|
