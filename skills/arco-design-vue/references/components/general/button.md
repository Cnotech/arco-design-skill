---
name: arco-vue-button
description: "Arco Design Vue 按钮 Button 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-button>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 按钮 Button

来源组件：上游 `web-vue/components/button`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-button>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
按钮分为 `primary` - **主要按钮**、`secondary` - **次要按钮（默认）**、`dashed` - **虚线按钮**、`outline` - **线形按钮**、`text` - **文本按钮**五种类型。




```vue
<template>
  <a-space>
    <a-button type="primary">Primary</a-button>
    <a-button>Secondary</a-button>
    <a-button type="dashed">Dashed</a-button>
    <a-button type="outline">Outline</a-button>
    <a-button type="text">Text</a-button>
  </a-space>
</template>
```

## 示例：图标按钮

### 说明
按钮可以嵌入图标。在只设置图标时，按钮的宽高相等。




```vue
<template>
  <a-space>
    <a-button type="primary">
      <template #icon>
        <icon-plus />
      </template>
    </a-button>
    <a-button type="primary">
      <template #icon>
        <icon-delete />
      </template>
      <!-- Use the default slot to avoid extra spaces -->
      <template #default>Delete</template>
    </a-button>
  </a-space>
</template>

<script>
import { IconPlus, IconDelete } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconPlus, IconDelete }
};
</script>
```

## 示例：按钮形状

### 说明
按钮分为 `square` - **长方形（默认）**、`circle` - **圆形**、`round` - **全圆角**三种形状。




```vue
<template>
  <a-space>
    <a-button type="primary">Square</a-button>
    <a-button type="primary" shape="round">Round</a-button>
    <a-button type="primary">
      <template #icon>
        <icon-plus />
      </template>
    </a-button>
    <a-button type="primary" shape="circle">
      <icon-plus />
    </a-button>
  </a-space>
</template>
<script>
import { IconPlus } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconPlus }
};
</script>
```

## 示例：按钮尺寸

### 说明
按钮分为 `mini`、`small`、`medium`、`large` 四种尺寸。高度分别为：`24px`、`28px`、`32px`、`36px`。推荐（默认）尺寸为 `medium`。可在不同场景及不同业务需求选择适合尺寸。




```vue
<template>
  <a-space>
    <a-button type="primary" size="mini">Mini</a-button>
    <a-button type="primary" size="small">Small</a-button>
    <a-button type="primary">Medium</a-button>
    <a-button type="primary" size="large">Large</a-button>
  </a-space>
</template>
```

## 示例：按钮状态

### 说明
按钮的状态分为 `normal` - **正常（默认）**、`success` - **成功**、`warning` - **警告**、`danger` - **危险**四种，可以与按钮类型同时使用。




```vue
<template>
  <a-space direction="vertical">
    <a-space>
      <a-button type="primary" status="success">Primary</a-button>
      <a-button status="success">Default</a-button>
      <a-button type="dashed" status="success">Dashed</a-button>
      <a-button type="outline" status="success">Outline</a-button>
      <a-button type="text" status="success">Text</a-button>
    </a-space>
    <a-space>
      <a-button type="primary" status="warning">Primary</a-button>
      <a-button status="warning">Default</a-button>
      <a-button type="dashed" status="warning">Dashed</a-button>
      <a-button type="outline" status="warning">Outline</a-button>
      <a-button type="text" status="warning">Text</a-button>
    </a-space>
    <a-space>
      <a-button type="primary" status="danger">Primary</a-button>
      <a-button status="danger">Default</a-button>
      <a-button type="dashed" status="danger">Dashed</a-button>
      <a-button type="outline" status="danger">Outline</a-button>
      <a-button type="text" status="danger">Text</a-button>
    </a-space>
  </a-space>
</template>
```

## 示例：禁用状态

### 说明
按钮的禁用状态。




```vue
<template>
  <a-space direction="vertical">
    <a-space>
      <a-button type="primary" disabled>Primary</a-button>
      <a-button disabled>Default</a-button>
      <a-button type="dashed" disabled>Dashed</a-button>
      <a-button type="outline" disabled>Outline</a-button>
      <a-button type="text" disabled>Text</a-button>
    </a-space>
    <a-space>
      <a-button type="primary" status="success" disabled>Primary</a-button>
      <a-button status="success" disabled>Default</a-button>
      <a-button type="dashed" status="success" disabled>Dashed</a-button>
      <a-button type="outline" status="success" disabled>Outline</a-button>
      <a-button type="text" status="success" disabled>Text</a-button>
    </a-space>
    <a-space>
      <a-button type="primary" status="warning" disabled>Primary</a-button>
      <a-button status="warning" disabled>Default</a-button>
      <a-button type="dashed" status="warning" disabled>Dashed</a-button>
      <a-button type="outline" status="warning" disabled>Outline</a-button>
      <a-button type="text" status="warning" disabled>Text</a-button>
    </a-space>
    <a-space>
      <a-button type="primary" status="danger" disabled>Primary</a-button>
      <a-button status="danger" disabled>Default</a-button>
      <a-button type="dashed" status="danger" disabled>Dashed</a-button>
      <a-button type="outline" status="danger" disabled>Outline</a-button>
      <a-button type="text" status="danger" disabled>Text</a-button>
    </a-space>
  </a-space>
</template>
```

## 示例：加载中状态

### 说明
通过设置 `loading` 可以让按钮处于加载中状态。处于加载中状态的按钮不会触发点击事件。




```vue
<template>
  <a-space>
    <a-button type="primary" loading>Primary</a-button>
    <a-button loading>Default</a-button>
    <a-button type="dashed" loading>Dashed</a-button>
    <a-button type="primary" :loading="loading1" @click="handleClick1">Click Me</a-button>
    <a-button type="primary" :loading="loading2" @click="handleClick2">
      <template #icon>
        <icon-plus />
      </template>
      Click Me
    </a-button>
  </a-space>
</template>

<script>
import { ref } from 'vue';
import { IconPlus } from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconPlus
  },
  setup() {
    const loading1 = ref(false);
    const loading2 = ref(false);

    const handleClick1 = () => {
      loading1.value = !loading1.value
    }
    const handleClick2 = () => {
      loading2.value = !loading2.value
    }

    return {
      loading1,
      loading2,
      handleClick1,
      handleClick2
    }
  }
}
</script>
```

## 示例：长按钮

### 说明
通过设置 `long` 属性，使按钮的宽度跟随容器的宽度。




```vue
<template>
  <a-space class="wrapper" direction="vertical">
    <a-button type="primary" long>Primary</a-button>
    <a-button long>Default</a-button>
    <a-button type="dashed" long>Dashed</a-button>
    <a-button type="outline" long>Outline</a-button>
    <a-button type="text" long>Text</a-button>
  </a-space>
</template>

<style scoped lang="less">
.wrapper{
  width: 400px;
  padding: 20px;
  border: 1px solid var(~'--color-border');
  border-radius: 4px;
}
</style>
```

## 示例：组合按钮

### 说明
通过 `<a-button-group>` 组件使按钮以组合方式出现。可用在同级多项操作中。




```vue
<template>
  <a-space direction="vertical">
    <a-button-group>
      <a-button>Publish</a-button>
      <a-button>
        <template #icon>
          <icon-down />
        </template>
      </a-button>
    </a-button-group>
    <a-button-group>
      <a-button>Publish</a-button>
      <a-button>
        <template #icon>
          <icon-more />
        </template>
      </a-button>
    </a-button-group>
    <a-button-group>
      <a-button type="primary">
        <icon-left />
        Prev
      </a-button>
      <a-button type="primary">
        Next
        <icon-right />
      </a-button>
    </a-button-group>
    <a-space size="large">
      <a-button-group type="primary">
        <a-button> copy </a-button>
        <a-button> cut </a-button>
        <a-button> find </a-button>
      </a-button-group>
      <a-button-group type="primary" status="warning">
        <a-button> <template #icon><icon-heart-fill /></template> </a-button>
        <a-button> <template #icon><icon-star-fill /></template> </a-button>
        <a-button> <template #icon><icon-thumb-up-fill /></template> </a-button>
      </a-button-group>
      <a-button-group size="small" disabled>
        <a-button> prev </a-button>
        <a-button> next </a-button>
      </a-button-group>
    </a-space>
  </a-space>
</template>
```

## API


### `<button>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|按钮的类型，分为五种：次要按钮、主要按钮、虚框按钮、线性按钮、文字按钮。|`ButtonTypes`|`'secondary'`|
|shape|按钮的形状|`BorderShape`|`-`|
|status|按钮的状态|`'normal' \| 'warning' \| 'success' \| 'danger'`|`'normal'`|
|size|按钮的尺寸|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`|
|long|按钮的宽度是否随容器自适应。|`boolean`|`false`|
|loading|按钮是否为加载中状态|`boolean`|`false`|
|disabled|按钮是否禁用|`boolean`|`false`|
|html-type|设置 `button` 的原生 `type` 属性，可选值参考 [HTML标准](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#attr-type "_blank")|`HTMLButtonElement['type']`|`'button'`|
|autofocus|设置 `button` 的原生 `autofocus` 属性，可选值参考 [HTML标准](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#attr-type "_blank")|`boolean`|`false`|
|href|设置跳转链接。设置此属性时，按钮渲染为a标签。|`string`|`-`|
### `<button>` 事件

|事件名|描述|参数|
|---|---|---|
|click|点击按钮时触发|ev: `MouseEvent`|
### `<button>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|icon|图标|-|




### `<button-group>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|按钮的类型，分为五种：次要按钮、主要按钮、虚框按钮、线性按钮、文字按钮。|`ButtonTypes`|`-`|
|status|按钮的状态|`'normal' \| 'warning' \| 'success' \| 'danger'`|`-`|
|shape|按钮的形状|`BorderShape`|`-`|
|size|按钮的尺寸|`'mini' \| 'small' \| 'medium' \| 'large'`|`-`|
|disabled|全部子按钮是否禁用|`boolean`|`false`|
