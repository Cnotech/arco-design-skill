---
name: arco-vue-grid
description: "Arco Design Vue 栅格 Grid 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-grid>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 栅格 Grid

来源组件：上游 `web-vue/components/grid`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-grid>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
展示了最基本的 24 等分应用。




```vue
<template>
  <div class="grid-demo-background">
    <a-space direction="vertical" :size="16" style="display: block;">
      <a-row class="grid-demo">
        <a-col :span="24">
          <div>24 - 100%</div>
        </a-col>
      </a-row>
      <a-row class="grid-demo">
        <a-col :span="12">
          <div>12 - 50%</div>
        </a-col>
        <a-col :span="12">
          <div>12 - 50%</div>
        </a-col>
      </a-row>
      <a-row class="grid-demo">
        <a-col :span="8">
          <div>8 - 33.33%</div>
        </a-col>
        <a-col :span="8">
          <div>8 - 33.33%</div>
        </a-col>
        <a-col :span="8">
          <div>8 - 33.33%</div>
        </a-col>
      </a-row>
      <a-row class="grid-demo">
        <a-col :span="6">
          <div>6 - 25%</div>
        </a-col>
        <a-col :span="6">
          <div>6 - 25%</div>
        </a-col>
        <a-col :span="6">
          <div>6 - 25%</div>
        </a-col>
        <a-col :span="6">
          <div>6 - 25%</div>
        </a-col>
      </a-row>
      <a-row class="grid-demo">
        <a-col :span="4">
          <div>4 - 16.66%</div>
        </a-col>
        <a-col :span="4">
          <div>4 - 16.66%</div>
        </a-col>
        <a-col :span="4">
          <div>4 - 16.66%</div>
        </a-col>
        <a-col :span="4">
          <div>4 - 16.66%</div>
        </a-col>
        <a-col :span="4">
          <div>4 - 16.66%</div>
        </a-col>
        <a-col :span="4">
          <div>4 - 16.66%</div>
        </a-col>
      </a-row>
    </a-space>
  </div>
</template>

<style scoped>
.grid-demo-background {
  background-image: linear-gradient(
    90deg,
    var(--color-fill-2) 4.16666667%,
    transparent 4.16666667%,
    transparent 8.33333333%,
    var(--color-fill-2) 8.33333333%,
    var(--color-fill-2) 12.5%,
    transparent 12.5%,
    transparent 16.66666667%,
    var(--color-fill-2) 16.66666667%,
    var(--color-fill-2) 20.83333333%,
    transparent 20.83333333%,
    transparent 25%,
    var(--color-fill-2) 25%,
    var(--color-fill-2) 29.16666667%,
    transparent 29.16666667%,
    transparent 33.33333333%,
    var(--color-fill-2) 33.33333333%,
    var(--color-fill-2) 37.5%,
    transparent 37.5%,
    transparent 41.66666667%,
    var(--color-fill-2) 41.66666667%,
    var(--color-fill-2) 45.83333333%,
    transparent 45.83333333%,
    transparent 50%,
    var(--color-fill-2) 50%,
    var(--color-fill-2) 54.16666667%,
    transparent 54.16666667%,
    transparent 58.33333333%,
    var(--color-fill-2) 58.33333333%,
    var(--color-fill-2) 62.5%,
    transparent 62.5%,
    transparent 66.66666667%,
    var(--color-fill-2) 66.66666667%,
    var(--color-fill-2) 70.83333333%,
    transparent 70.83333333%,
    transparent 75%,
    var(--color-fill-2) 75%,
    var(--color-fill-2) 79.16666667%,
    transparent 79.16666667%,
    transparent 83.33333333%,
    var(--color-fill-2) 83.33333333%,
    var(--color-fill-2) 87.5%,
    transparent 87.5%,
    transparent 91.66666667%,
    var(--color-fill-2) 91.66666667%,
    var(--color-fill-2) 95.83333333%,
    transparent 95.83333333%
  );
}
.grid-demo .arco-col {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}
.grid-demo .arco-col:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo .arco-col:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：栅格偏移

### 说明
指定 `offset` 可以对栅格进行平移操作。




```vue
<template>
  <div>
    <a-row class="grid-demo" style="marginBottom: 16px; backgroundColor: var(--color-fill-2);">
      <a-col :span="8">col - 8</a-col>
      <a-col :span="8" :offset="8">
        col - 8 | offset - 8
      </a-col>
    </a-row>
    <a-row class="grid-demo" style="marginBottom: 16px; backgroundColor: var(--color-fill-2);">
      <a-col :span="6" :offset="8">
        col - 6 | offset - 8
      </a-col>
      <a-col :span="6" :offset="4">
        col - 6 | offset - 4
      </a-col>
    </a-row>
    <a-row class="grid-demo" style="backgroundColor: var(--color-fill-2)">
      <a-col :span="12" :offset="8">
        col - 12 | offset - 8
      </a-col>
    </a-row>
  </div>
</template>

<style scoped>
.grid-demo .arco-col {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}
.grid-demo .arco-col:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo .arco-col:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：区块间隔

### 说明
通过在 `Row` 上指定 `gutter` 可以增加栅格的区域间隔。




```vue
<template>
  <div>
    <p>Horizontal</p>
    <a-row class="grid-demo" :gutter="24">
      <a-col :span="12">
        <div>col - 12</div>
      </a-col>
      <a-col :span="12">
        <div>col - 12</div>
      </a-col>
    </a-row>
    <p>Responsive</p>
    <a-row class="grid-demo" :gutter="{ md: 8, lg: 24, xl: 32 }">
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
    </a-row>
    <p>Horizontal and Vertical</p>
    <a-row class="grid-demo" :gutter="[24, 12]">
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
    </a-row>
  </div>
</template>

<style scoped>
.grid-demo .arco-col {
  height: 48px;
  color: var(--color-white);
}
.grid-demo .arco-col > div {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.grid-demo .arco-col:nth-child(2n) > div {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo .arco-col:nth-child(2n + 1) > div {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：水平布局

### 说明
通过 `justify` 来进行水平布局。




```vue
<template>
  <div>
    <p>Arrange left</p>
    <a-row class="grid-demo" justify="start">
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
    </a-row>
    <p>Arrange center</p>
    <a-row class="grid-demo" justify="center">
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
    </a-row>
    <p>Arrange right</p>
    <a-row class="grid-demo" justify="end">
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
    </a-row>
    <p>Space around</p>
    <a-row class="grid-demo" justify="space-around">
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
    </a-row>
    <p>Space between</p>
    <a-row class="grid-demo" justify="space-between">
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
      <a-col :span="4">
        <div>col - 4</div>
      </a-col>
    </a-row>
  </div>
</template>

<style scoped>
.grid-demo {
  background-color: var(--color-fill-2);
  margin-bottom: 40px;
}
.grid-demo:last-child {
  margin-bottom: 0px;
}
.grid-demo .arco-col {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}
.grid-demo .arco-col:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo .arco-col:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：垂直布局

### 说明
通过 `align` 来进行垂直布局。




```vue
<template>
  <div>
    <p>Arrange top</p>
    <a-row class="grid-demo" align="start">
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
    </a-row>
    <p>Arrange center</p>
    <a-row class="grid-demo" align="center">
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
    </a-row>
    <p>Arrange bottom</p>
    <a-row class="grid-demo" align="end">
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
      <a-col :span="6">
        <div>col - 6</div>
      </a-col>
    </a-row>
  </div>
</template>

<style scoped>
.grid-demo {
  background-color: var(--color-fill-2);
  margin-bottom: 40px;
}
.grid-demo:last-child {
  margin-bottom: 0px;
}
.grid-demo .arco-col {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}
.grid-demo .arco-col:nth-of-type(1) {
  height: 90px;
  line-height: 90px;
}
.grid-demo .arco-col:nth-of-type(2) {
  height: 48px;
  line-height: 48px;
}
.grid-demo .arco-col:nth-of-type(3) {
  height: 120px;
  line-height: 120px;
}
.grid-demo .arco-col:nth-of-type(4) {
  height: 60px;
  line-height: 60px;
}
.grid-demo .arco-col:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo .arco-col:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：排序

### 说明
通过 `order` 来进行元素排序。




```vue
<template>
  <div>
    <a-row class="grid-demo">
      <a-col :span="6" :order="4">
        <div>1 col-order-4</div>
      </a-col>
      <a-col :span="6" :order="3">
        <div>2 col-order-3</div>
      </a-col>
      <a-col :span="6" :order="2">
        <div>3 col-order-2</div>
      </a-col>
      <a-col :span="6" :order="1">
        <div>4 col-order-1</div>
      </a-col>
    </a-row>
  </div>
</template>

<style scoped>
.grid-demo .arco-col {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}
.grid-demo .arco-col:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo .arco-col:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：响应式布局

### 说明
预置六种响应尺寸, 分别为 `xs`, `sm`, `md`, `lg`, `xl`, `xxl`。




```vue
<template>
  <a-row class="grid-demo">
    <a-col :xs="2" :sm="4" :md="6" :lg="8" :xl="10" :xxl="8">
      Col
    </a-col>
    <a-col :xs="20" :sm="16" :md="12" :lg="8" :xl="4" :xxl="8">
      Col
    </a-col>
    <a-col :xs="2" :sm="4" :md="6" :lg="8" :xl="10" :xxl="8">
      Col
    </a-col>
  </a-row>
</template>

<style scoped>
.grid-demo .arco-col {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}
.grid-demo .arco-col:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo .arco-col:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：其他属性的响应式

### 说明
`span`, `offset`, `order` 属性可以内嵌到 `xs`, `sm`, `md`, `lg`, `xl`, `xxl` 对象中使用。
比如 `:xs="8"` 相当于 `:xs="{ span: 8 }"`。




```vue
<template>
  <div>
    <a-row class="grid-demo">
      <a-col :xs="{span: 5, offset: 1}" :lg="{span: 6, offset: 2}">
        Col
      </a-col>
      <a-col :xs="{span: 11, offset: 1}" :lg="{span: 6, offset: 2}">
        Col
      </a-col>
      <a-col :xs="{span: 5, offset: 1}" :lg="{span: 6, offset: 2}">
        Col
      </a-col>
    </a-row>
  </div>
</template>

<style scoped>
.grid-demo .arco-col {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}
.grid-demo .arco-col:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo .arco-col:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：Flex 用法

### 说明
通过设置 `Col` 组件的 `flex` 属性，可以任意配置 flex 布局。




```vue
<template>
  <a-row class="grid-demo" style="margin-bottom: 16px;">
    <a-col flex="100px">
      <div>100px</div>
    </a-col>
    <a-col flex="auto">
      <div>auto</div>
    </a-col>
  </a-row>
  <a-row class="grid-demo" style="margin-bottom: 16px;">
    <a-col flex="100px">
      <div>100px</div>
    </a-col>
    <a-col flex="auto">
      <div>auto</div>
    </a-col>
    <a-col flex="100px">
      <div>100px</div>
    </a-col>
  </a-row>
  <a-row class="grid-demo" style="margin-bottom: 16px;">
    <a-col :flex="3">
      <div>3 / 12</div>
    </a-col>
    <a-col :flex="4">
      <div>4 / 12</div>
    </a-col>
    <a-col :flex="5">
      <div>5 / 12</div>
    </a-col>
  </a-row>
</template>

<style scoped>
.grid-demo .arco-col {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}

.grid-demo .arco-col:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}

.grid-demo .arco-col:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
</style>
```

## 示例：Grid 布局

### 说明
基于 CSS 的 Grid 布局实现的布局组件，支持折叠，并且可以设置后缀节点，后缀节点会显示在一行的结尾。




```vue

<template>
  <div style="margin-bottom: 20px;">
    <a-typography-text>折叠：</a-typography-text>
    <a-switch :checked="collapsed" @click="collapsed = !collapsed" />
  </div>
  <a-grid :cols="3" :colGap="12" :rowGap="16" class="grid-demo-grid" :collapsed="collapsed">
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item" :offset="1">item | offset - 1</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item" :span="3">item | span - 3</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item" suffix #="{ overflow }">
      suffix | overflow: {{ overflow }}
    </a-grid-item>
  </a-grid>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const collapsed = ref(false);

    return {
      collapsed
    }
  },
}
</script>

<style scoped>
.grid-demo-grid .demo-item,
.grid-demo-grid .demo-suffix {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}

.grid-demo-grid .demo-item:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}

.grid-demo-grid .demo-item:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## 示例：响应式的 Grid 布局

### 说明
Grid 组件的响应式配置格式为 `{ xs: 1, sm: 2, md: 3, lg: 4, xl: 5, xxl: 6 }`。




```vue
<template>
  <a-grid :cols="{ xs: 1, sm: 2, md: 3, lg: 4, xl: 5, xxl: 6 }" :colGap="12" :rowGap="16" class="grid-demo-grid">
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item">item</a-grid-item>
    <a-grid-item class="demo-item" :span="{ xl: 4, xxl: 6 }" suffix>
      suffix
    </a-grid-item>
  </a-grid>
</template>

<style scoped>
.grid-demo-grid .demo-item,
.grid-demo-grid .demo-suffix {
  height: 48px;
  line-height: 48px;
  color: var(--color-white);
  text-align: center;
}
.grid-demo-grid .demo-item:nth-child(2n) {
  background-color: rgba(var(--arcoblue-6), 0.9);
}
.grid-demo-grid .demo-item:nth-child(2n + 1) {
  background-color: var(--color-primary-light-4);
}
</style>
```

## API


### `<row>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|gutter|栅格间隔，单位是`px` 栅格间隔。可传入响应式对象写法 { xs: 4, sm: 6, md: 12}，传入数组 [ 水平间距， 垂直间距 ] 来设置两个方向。|`number\| ResponsiveValue\| [number \| ResponsiveValue, number \| ResponsiveValue]`|`0`||
|justify|水平对齐方式 (`justify-content`)|`'start' \| 'center' \| 'end' \| 'space-around' \| 'space-between'`|`'start'`||
|align|竖直对齐方式 ( `align-items` )|`'start' \| 'center' \| 'end' \| 'stretch'`|`'start'`||
|div|开启这个选项`Row`和`Col`都会被当作div而不会附带任何Grid相关的类和样式|`boolean`|`false`||
|wrap|`Col` 是否支持换行|`boolean`|`true`|2.13.0|




### `<col>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|span|栅格占位格数|`number`|`24`||
|offset|栅格左侧的间隔格数，间隔内不可以有栅格|`number`|`-`||
|order|对元素进行排序|`number`|`-`||
|xs|< 576px 响应式栅格|`number \| { [key: string]: any }`|`-`||
|sm|>= 576px 响应式栅格|`number \| { [key: string]: any }`|`-`||
|md|>= 768px 响应式栅格|`number \| { [key: string]: any }`|`-`||
|lg|>= 992px 响应式栅格|`number \| { [key: string]: any }`|`-`||
|xl|>= 1200px 响应式栅格|`number \| { [key: string]: any }`|`-`||
|xxl|>= 1600px 响应式栅格|`number \| { [key: string]: any }`|`-`||
|flex|设置 flex 布局属性|`number \| string \| 'initial' \| 'auto' \| 'none'`|`-`|2.10.0|




### `<grid>` 属性 (2.15.0)
响应式配置从 `2.18.0` 开始支持，具体配置 [ResponsiveValue](#responsivevalue)

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|cols|每一行展示的列数|`number \| ResponsiveValue`|`24`|
|row-gap|行与行之间的间距|`number \| ResponsiveValue`|`0`|
|col-gap|列与列之间的间距|`number \| ResponsiveValue`|`0`|
|collapsed|是否折叠|`boolean`|`false`|
|collapsed-rows|折叠时显示的行数|`number`|`1`|




### `<grid-item>` 属性 (2.15.0)
响应式配置从 `2.18.0` 开始支持，具体配置 [ResponsiveValue](#responsivevalue)

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|span|跨越的格数|`number \| ResponsiveValue`|`1`|
|offset|左侧的间隔格数|`number \| ResponsiveValue`|`0`|
|suffix|是否是后缀元素|`boolean`|`false`|




### ResponsiveValue

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|xxl|>= 1600px 响应式配置|`number`|`-`|
|xl|>= 1200px 响应式配置|`number`|`-`|
|lg|>= 992px 响应式配置|`number`|`-`|
|md|>= 768px 响应式配置|`number`|`-`|
|sm|>= 576px 响应式配置|`number`|`-`|
|xs|< 576px 响应式配置|`number`|`-`|
