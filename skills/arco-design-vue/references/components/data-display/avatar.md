---
name: arco-vue-avatar
description: "Arco Design Vue 头像 Avatar 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-avatar>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 头像 Avatar

来源组件：上游 `web-vue/components/avatar`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-avatar>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
头像的基础使用。如果头像是文字的话，会自动调节字体大小，来适应头像框。




```vue
<template>
  <a-space size="large">
    <a-avatar>A</a-avatar>
    <a-avatar :style="{ backgroundColor: '#3370ff' }">
      <IconUser />
    </a-avatar>
    <a-avatar :style="{ backgroundColor: '#14a9f8' }">Arco</a-avatar>
    <a-avatar :style="{ backgroundColor: '#00d0b6' }">Design</a-avatar>
    <a-avatar>
      <img
        alt="avatar"
        src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp"
      />
    </a-avatar>
  </a-space>
</template>

<script>
import { IconUser } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconUser },
};
</script>
```

## 示例：大小和形状

### 说明
通过设置 `size` 字段，可以调节头像的大小，默认大小为 `40px`。设置 `shape` 字段，可以设置头像是圆形 (circle) 还是正方形 (square)。




```vue
<template>
  <a-space size="large" direction="vertical">
    <a-space size="large">
      <a-avatar :size="64">Arco</a-avatar>
      <a-avatar :size="40">Arco</a-avatar>
      <a-avatar :size="32">Arco</a-avatar>
      <a-avatar :size="24">Arco</a-avatar>
    </a-space>
    <a-space size="large">
      <a-avatar :size="64" shape="square">Arco</a-avatar>
      <a-avatar :size="40" shape="square">Arco</a-avatar>
      <a-avatar :size="32" shape="square">Arco</a-avatar>
      <a-avatar :size="24" shape="square">Arco</a-avatar>
    </a-space>
  </a-space>
</template>
```

## 示例：头像组

### 说明
使用 `Avatar.Group` 可以使用头像组功能，可通过 `size` 指定头像的大小。




```vue
<template>
  <a-space :size="32">
    <a-avatar-group>
      <a-avatar :style="{ backgroundColor: '#7BC616' }">A</a-avatar>
      <a-avatar :style="{ backgroundColor: '#14C9C9' }">B</a-avatar>
      <a-avatar :style="{ backgroundColor: '#168CFF' }">C</a-avatar>
      <a-avatar :style="{ backgroundColor: '#FF7D00' }">Arco</a-avatar>
      <a-avatar :style="{ backgroundColor: '#FFC72E' }">Design</a-avatar>
    </a-avatar-group>

    <a-avatar-group :size="24">
      <a-avatar :style="{ backgroundColor: '#7BC616' }">A</a-avatar>
      <a-avatar :style="{ backgroundColor: '#14C9C9' }">B</a-avatar>
      <a-avatar :style="{ backgroundColor: '#168CFF' }">C</a-avatar>
      <a-avatar :style="{ backgroundColor: '#FF7D00' }">Arco</a-avatar>
      <a-avatar :style="{ backgroundColor: '#FFC72E' }">Design</a-avatar>
    </a-avatar-group>

    <a-avatar-group :size="24" :max-count="3">
      <a-avatar :style="{ backgroundColor: '#7BC616' }">A</a-avatar>
      <a-avatar :style="{ backgroundColor: '#14C9C9' }">B</a-avatar>
      <a-avatar :style="{ backgroundColor: '#168CFF' }">C</a-avatar>
      <a-avatar :style="{ backgroundColor: '#FF7D00' }">Arco</a-avatar>
      <a-avatar :style="{ backgroundColor: '#FFC72E' }">Design</a-avatar>
    </a-avatar-group>
  </a-space>
</template>
```

## 示例：交互按钮

### 说明
可以通过 `trigger-icon` `trigger-type` 来定制交互按钮，类型有 `mask (遮罩)` 和 `button (按钮)` 两种。




```vue
<template>
  <a-space size="large">
    <a-avatar
      :trigger-icon-style="{ color: '#3491FA' }"
      :auto-fix-font-size="false"
      @click="toast"
      :style="{ backgroundColor: '#168CFF' }"
    >
      A
      <template #trigger-icon>
        <IconCamera />
      </template>
    </a-avatar>
    <a-avatar @click="toast" :style="{ backgroundColor: '#14C9C9' }">
      <IconUser />
      <template #trigger-icon>
        <IconEdit />
      </template>
    </a-avatar>
    <a-avatar
      @click="toast"
      shape="square"
      :style="{ backgroundColor: '#FFC72E' }"
    >
      <IconUser />
      <template #trigger-icon>
        <IconEdit />
      </template>
    </a-avatar>
    <a-avatar trigger-type="mask">
      <img
        alt="avatar"
        src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp"
      />
      <template #trigger-icon>
        <IconEdit />
      </template>
    </a-avatar>
  </a-space>
</template>

<script>
import { IconCamera, IconEdit, IconUser } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconCamera, IconEdit },
  methods: {
    toast() {
      this.$message.info('Uploading...');
    },
  },
};
</script>
```

## 示例：自动调整字体大小

### 说明
如果头像是文字的话，会自动调节字体大小，来适应头像框。




```vue

<template>
  <a-avatar
    :style="{
      marginRight: '24px',
      verticalAlign: 'middle',
      backgroundColor: '#14a9f8',
    }"
  >
    {{ text }}
  </a-avatar>
  <a-button
    type="secondary"
    @click="onClick"
    :style="{ verticalAlign: 'middle' }"
  >
    Change
  </a-button>
</template>

<script>
import { computed, ref } from 'vue';

const list = ['B', 'Arco', 'Design', 'Tom', 'AD'];
export default {
  setup() {
    const index = ref(0);
    const text = computed(() => list[index.value])

    const onClick = () => {
      index.value = index.value >= list.length - 1 ? 0 : index.value + 1;
    };

    return {
      text,
      onClick
    }
  },
};
</script>
```

## 示例：自定义头像路径

### 说明
自定义头像图片路径




```vue
<template>
  <a-space size="large">
    <a-avatar
      imageUrl="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp"
    >
    </a-avatar>
    加载失败:
    <a-avatar
      imageUrl="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9123.png~tplv-uwbnlip3yd-webp.webp"
    >
    </a-avatar>
  </a-space>
</template>
```

## API


### `<avatar>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|shape|头像的形状，有圆形(circle)和正方形(square)两种|`'circle' \| 'square'`|`'circle'`||
|image-url|自定义头像图片地址，如果传入该属性，会默认渲染img标签|`string`|`-`|2.40.0|
|size|头像的尺寸大小，单位是 `px`。未填写时使用样式中的大小 `40px`|`number`|`-`||
|auto-fix-font-size|是否自动根据头像尺寸调整字体大小|`boolean`|`true`||
|trigger-type|可点击的头像交互类型|`'mask' \| 'button'`|`'button'`||
|trigger-icon-style|交互图标的样式|`CSSProperties`|`-`||
|object-fit|图片在容器内的的适应类型|`ObjectFit`|`-`|2.52.0|
### `<avatar>` 事件

|事件名|描述|参数|
|---|---|---|
|click|点击回调|ev: `MouseEvent`|
|error|图片加载错误|-|
|load|图片加载成功|-|
### `<avatar>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|trigger-icon|可点击的头像交互图标|-|




### `<avatar-group>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|shape|头像的形状，有圆形(circle)和正方形(square)两种|`'circle' \| 'square'`|`'circle'`||
|size|头像的尺寸大小，单位是 `px`|`number`|`-`||
|auto-fix-font-size|是否自动根据头像尺寸调整字体大小|`boolean`|`true`||
|max-count|头像组最多显示的头像数量，多余头像将以 `+x` 的形式展示。|`number`|`0`||
|z-index-ascend|头像组内的头像 `z-index` 递增，默认是递减。|`boolean`|`false`||
|max-style|多余头像样式。|`CSSProperties`|`-`|2.7.0|
|max-popover-trigger-props|多余头像气泡的 `TriggerProps`|`TriggerProps`|`-`|2.7.0|
