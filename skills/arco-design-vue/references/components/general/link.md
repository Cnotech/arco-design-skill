---
name: arco-vue-link
description: "Arco Design Vue 链接 Link 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-link>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 链接 Link

来源组件：上游 `web-vue/components/link`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-link>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
链接的基本用法。




```vue
<template>
  <a-space>
    <a-link href="link">Link</a-link>
    <a-link href="link" disabled>Link</a-link>
  </a-space>
</template>
```

## 示例：链接的状态

### 说明
链接的状态分为 `normal` - **正常（默认）**、`success` - **成功**、`warning` - **警告**、`danger` - **危险**四种。




```vue
<template>
  <a-space direction="vertical">
    <a-space>
      <a-link href="link">Normal Link</a-link>
      <a-link href="link" disabled>Normal Link</a-link>
    </a-space>
    <a-space>
      <a-link href="link" status="success">Success Link</a-link>
      <a-link href="link" status="success" disabled>Success Link</a-link>
    </a-space>
    <a-space>
      <a-link href="link" status="warning">Warning Link</a-link>
      <a-link href="link" status="warning" disabled>Warning Link</a-link>
    </a-space>
    <a-space>
      <a-link href="link" status="danger">Danger Link</a-link>
      <a-link href="link" status="danger" disabled>Danger Link</a-link>
    </a-space>
  </a-space>
</template>
```

## 示例：悬浮状态底色

### 说明
可以通过 hoverable 属性设置是否在悬浮状态时隐藏底色。





```vue
<template>
  <a-space>
    <a-link href="link" :hoverable="false">Link</a-link>
    <a-link href="link" status="danger" :hoverable="false">Link</a-link>
  </a-space>
</template>
```

## 示例：图标

### 说明
通过 `icon` 设置带图标的链接，设置为 `true` 时候显示默认图标。




```vue
<template>
  <div>
    <a-space>
      <a-link href="link" icon>Link</a-link>
      <a-link href="link" disabled icon>Link</a-link>
    </a-space>
  </div>
  <div>
    <a-space>
      <a-link href="link">
        <template #icon>
          <icon-edit />
        </template>
        Link
      </a-link>
      <a-link href="link" disabled>
        <template #icon>
          <icon-edit />
        </template>
        Link
      </a-link>
    </a-space>
  </div>
</template>

<script>
  import { IconEdit } from '@arco-design/web-vue/es/icon';

  export default {
    components: { IconEdit }
  };
</script>
```

## 示例：加载中状态

### 说明
通过设置 `loading` 可以让链接处于加载中状态。处于加载中状态的链接不会触发点击事件。




```vue
<template>
  <a-space>
    <a-link loading>Link</a-link>
    <a-link :loading="loading1" @click="handleClick1">Link</a-link>
    <a-link :loading="loading2" @click="handleClick2">
      <template #icon>
        <icon-edit />
      </template>
      Link
    </a-link>
  </a-space>
</template>

<script>
import { ref } from 'vue';
import { IconEdit } from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconEdit,
  },
  setup() {
    const loading1 = ref(false);
    const loading2 = ref(false);

    const handleClick1 = () => {
      loading1.value = true;
      setTimeout(() => {
        loading1.value = false;
      }, 3000);
    }
    const handleClick2 = () => {
      loading2.value = true;
      setTimeout(() => {
        loading2.value = false;
      }, 3000);
    }

    return {
      loading1,
      loading2,
      handleClick1,
      handleClick2,
    };
  }
}
</script>
```

## API



### `<link>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|href|链接地址|`string`|`-`||
|status|链接的状态|`'normal' \| 'warning' \| 'success' \| 'danger'`|`'normal'`||
|hoverable|鼠标悬浮时存在底色|`boolean`|`true`|2.7.0|
|icon|图标|`boolean`|`false`|2.7.0|
|loading|链接是否为加载中状态|`boolean`|`false`|2.37.0|
|disabled|链接是否禁用|`boolean`|`false`||
### `<link>` 事件

|事件名|描述|参数|
|---|---|---|
|click|点击时触发|ev: `MouseEvent`|
