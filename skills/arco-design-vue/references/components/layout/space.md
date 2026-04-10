---
name: arco-vue-space
description: "Arco Design Vue 间距 Space 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-space>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 间距 Space

来源组件：上游 `web-vue/components/space`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-space>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
间距组件的基本用法。




```vue
<template>
  <a-space>
    <a-typography-text>Space:</a-typography-text>
    <a-tag v-if="false" color='arcoblue'>Tag</a-tag>
    <a-button type="primary">Item1</a-button>
    <a-button type="primary">Item2</a-button>
    <a-switch defaultChecked />
  </a-space>
</template>
```

## 示例：垂直间距

### 说明
可以设置垂直方向排列的间距。




```vue
<template>
  <a-space direction="vertical" fill>
    <a-button type="primary" long>Item1</a-button>
    <a-button type="primary" long>Item2</a-button>
    <a-button type="primary" long>Item3</a-button>
  </a-space>
</template>
```

## 示例：尺寸

### 说明
内置 4 个尺寸，`mini - 4px` `small - 8px (默认)` `medium - 16px` `large - 24px`，也支持传数字来自定义尺寸。




```vue
<template>
  <div>
    <div style="marginBottom: 20px">
      <a-radio-group v-model="size" type='button'>
        <a-radio value="mini">mini</a-radio>
        <a-radio value="small">small</a-radio>
        <a-radio value="medium">medium</a-radio>
        <a-radio value="large">large</a-radio>
      </a-radio-group>
    </div>
    <a-space :size="size">
      <a-button type="primary">Item1</a-button>
      <a-button type="primary">Item2</a-button>
      <a-button type="primary">Item3</a-button>
    </a-space>
  </div>
</template>
<script>
export default {
  data() {
    return {
      size: 'medium',
    }
  }
};
</script>
```

## 示例：对齐

### 说明
内置 4 种对齐方式，分别为 `start` `center` `end` `baseline`，在水平模式下默认为 `center`。




```vue
<template>
  <div>
    <div style="marginBottom: 20px">
      <a-radio-group v-model="align" type='button'>
        <a-radio value="start">start</a-radio>
        <a-radio value="center">center</a-radio>
        <a-radio value="end">end</a-radio>
        <a-radio value="baseline">baseline</a-radio>
      </a-radio-group>
    </div>
    <a-space :align="align" style="backgroundColor: var(--color-fill-2);padding: 10px;">
      <a-typography-text>Space:</a-typography-text>
      <a-button type="primary">Item2</a-button>
      <a-card title='Card'>
        Card content
      </a-card>
    </a-space>
  </div>
</template>
<script>
export default {
  data() {
    return {
      align: 'center',
    }
  }
};
</script>
```

## 示例：环绕间距

### 说明
环绕类型的间距，四周都有间距，一般用于换行的场景。




```vue
<template>
  <a-space wrap>
    <a-button type="primary">Item1</a-button>
    <a-button type="primary">Item2</a-button>
    <a-button type="primary">Item3</a-button>
    <a-button type="primary">Item4</a-button>
    <a-button type="primary">Item5</a-button>
    <a-button type="primary">Item6</a-button>
    <a-button type="primary">Item7</a-button>
    <a-button type="primary">Item8</a-button>
    <a-button type="primary">Item9</a-button>
    <a-button type="primary">Item10</a-button>
    <a-button type="primary">Item11</a-button>
    <a-button type="primary">Item12</a-button>
    <a-button type="primary">Item13</a-button>
    <a-button type="primary">Item14</a-button>
    <a-button type="primary">Item15</a-button>
    <a-button type="primary">Item16</a-button>
    <a-button type="primary">Item17</a-button>
    <a-button type="primary">Item18</a-button>
    <a-button type="primary">Item19</a-button>
    <a-button type="primary">Item20</a-button>
  </a-space>
</template>
```

## 示例：分隔符

### 说明
为相邻子元素设置分隔符。




```vue
<template>
  <a-space>
    <template #split>
      <a-divider direction="vertical" :margin="0" />
    </template>
    <a-button type="primary">Item1</a-button>
    <a-tag v-if="show" color='arcoblue'>Tag</a-tag>
    <a-button type="primary">Item2</a-button>
    <a-button type="primary">Item3</a-button>
    <a-switch v-model="show"/>
  </a-space>
  <a-divider />
  <a-space>
    <template #split>
      <a-divider direction="vertical" :margin="0" />
    </template>
    <a-link type="primary">Link1</a-link>
    <a-link type="primary">Link2</a-link>
    <a-link type="primary">Link3</a-link>
  </a-space>
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
</script>
```

## API


### `<space>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|align|对齐方式|`'start' \| 'end' \| 'center' \| 'baseline'`|`-`||
|direction|间距方向|`'vertical' \| 'horizontal'`|`'horizontal'`||
|size|间距大小，支持分别制定横向和竖向的间距|`number \| 'mini' \| 'small' \| 'medium' \| 'large' \| [SpaceSize, SpaceSize]`|`'small'`||
|wrap|环绕类型的间距，用于折行的场景。|`boolean`|`false`||
|fill|充满整行|`boolean`|`false`|2.11.0|
### `<space>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|split|设置分隔符|-|



## Type
```ts
type SpaceSize = number | 'mini' | 'small' | 'medium' | 'large';
```
