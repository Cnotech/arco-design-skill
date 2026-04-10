---
name: arco-vue-tag
description: "Arco Design Vue 标签 Tag 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-tag>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 标签 Tag

来源组件：上游 `web-vue/components/tag`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-tag>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
标签的基本用法




```vue
<template>
  <a-space>
    <a-tag>Default</a-tag>
    <a-tag>Tag 1</a-tag>
    <a-tag>Tag 2</a-tag>
    <a-tag>
      <template #icon>
        <icon-check-circle-fill />
      </template>
      Complete
    </a-tag>
  </a-space>
</template>
```

## 示例：可关闭标签

### 说明
通过 `closable` 属性控制标签是否可关闭。可关闭标签可通过 `close` 事件执行一些关闭后操作，也可通过 `visible` 属性控制标签的显示或隐藏。




```vue
<template>
  <a-space>
    <a-tag closable>Tag</a-tag>
    <a-tag closable>
      <template #icon>
        <icon-star/>
      </template>
      Tag
    </a-tag>
  </a-space>
</template>
```

## 示例：动态编辑标签

### 说明
可动态添加和删除标签。




```vue
<template>
  <a-space wrap>
    <a-tag
      v-for="(tag, index) of tags"
      :key="tag"
      :closable="index !== 0"
      @close="handleRemove(tag)"
    >
      {{ tag }}
    </a-tag>

    <a-input
      v-if="showInput"
      ref="inputRef"
      :style="{ width: '90px'}"
      size="mini"
      v-model.trim="inputVal"
      @keyup.enter="handleAdd"
      @blur="handleAdd"
    />
    <a-tag
      v-else
      :style="{
        width: '90px',
        backgroundColor: 'var(--color-fill-2)',
        border: '1px dashed var(--color-fill-3)',
        cursor: 'pointer',
      }"
      @click="handleEdit"
    >
      <template #icon>
        <icon-plus />
      </template>
      Add Tag
    </a-tag>
  </a-space>
</template>

<script>
import { ref, nextTick } from 'vue';

export default {
  setup() {
    const tags = ref(['Tag 1', 'Tag 2', 'Tag 3']);
    const inputRef = ref(null);
    const showInput = ref(false);
    const inputVal = ref('');

    const handleEdit = () => {
      showInput.value = true;

      nextTick(() => {
        if (inputRef.value) {
          inputRef.value.focus();
        }
      });
    };

    const handleAdd = () => {
      if (inputVal.value) {
        tags.value.push(inputVal.value);
        inputVal.value = '';
      }
      showInput.value = false;
    };

    const handleRemove = (key) => {
      tags.value = tags.value.filter((tag) => tag !== key);
    };

    return {
      tags,
      inputRef,
      showInput,
      inputVal,
      handleEdit,
      handleAdd,
      handleRemove,
    };
  },
};
</script>

```

## 示例：可选中

### 说明
通过设置 `checkable` ，可以实现点击选中的效果。




```vue
<template>
  <a-space>
    <a-tag checkable>Awesome</a-tag>
    <a-tag checkable color="red" :default-checked="true">Toutiao</a-tag>
    <a-tag checkable color="arcoblue" :default-checked="true">Lark</a-tag>
  </a-space>
</template>
```

## 示例：标签的颜色

### 说明
我们提供多种预设色彩的标签样式，通过 `color` 设置不同颜色。如果预设值不能满足你的需求，`color` 字段也可以设置自定义色值。




```vue
<template>
  <a-space wrap>
    <a-tag v-for="(color, index) of colors" :key="index" :color="color" closable>{{ color }}</a-tag>
  </a-space>
  <h3>Custom Color:</h3>
  <a-space wrap>
    <a-tag v-for="(color, index) of custom" :key="index" :color="color" closable>{{ color }}</a-tag>
  </a-space>
</template>

<script>
export default {
  setup() {
    const colors = [
      'red',
      'orangered',
      'orange',
      'gold',
      'lime',
      'green',
      'cyan',
      'blue',
      'arcoblue',
      'purple',
      'pinkpurple',
      'magenta',
      'gray'
    ];
    const custom = [
      '#f53f3f',
      '#7816ff',
      '#00b42a',
      '#165dff',
      '#ff7d00',
      '#eb0aa4',
      '#7bc616',
      '#86909c',
      '#b71de8',
      '#0fc6c2',
      '#ffb400',
      '#168cff',
      '#ff5722'
    ];

    return {
      colors,
      custom
    }
  },
}
</script>
```

## 示例：标签的尺寸

### 说明
标签的大小分为：`small`、`medium`、`large` 三种，可以在不同场景下选择合适按钮尺寸。推荐及默认尺寸为 `medium`。




```vue
<template>
  <a-space>
    <a-tag size="large">Large</a-tag>
    <a-tag>Medium</a-tag>
    <a-tag size="small">Small</a-tag>
  </a-space>
</template>
```

## 示例：加载中状态

### 说明
标签的加载中状态。




```vue
<template>
  <a-tag loading>Loading</a-tag>
</template>
```

## 示例：带图标的标签

### 说明
可通过 `icon` 插槽在标签中加入图标。




```vue
<template>
  <a-space>
    <a-tag color="gray">
      <template #icon>
        <icon-github/>
      </template>
      Github
    </a-tag>
    <a-tag color="orangered">
      <template #icon>
        <icon-gitlab/>
      </template>
      Gitlab
    </a-tag>
    <a-tag color="blue">
      <template #icon>
        <icon-twitter/>
      </template>
      Twitter
    </a-tag>
    <a-tag color="arcoblue">
      <template #icon>
        <icon-facebook/>
      </template>
      Facebook
    </a-tag>
  </a-space>
</template>
```

## 示例：带边框的标签

### 说明
通过参数 `bordered`，可以显示带边框的标签。




```vue
<template>
   <a-space wrap>
    <a-tag bordered>default</a-tag>
    <a-tag v-for="(color, index) of colors" :key="index" :color="color" bordered>{{ color }}</a-tag>
  </a-space>
</template>

<script>
export default {
  setup() {
    const colors = [
      'orangered',
      'orange',
      'gold',
      'lime',
      'green',
      'cyan',
      'blue',
      'arcoblue',
      'purple',
      'pinkpurple',
      'magenta',
      'gray'
    ];
    return {
      colors
    }
  },
}
</script>
```

## API


### `<tag>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|color|标签的颜色|`'red' \| 'orangered' \| 'orange' \| 'gold' \| 'lime' \| 'green' \| 'cyan' \| 'blue' \| 'arcoblue' \| 'purple' \| 'pinkpurple' \| 'magenta' \| 'gray'`|`-`||
|size|标签的大小|`'small' \| 'medium' \| 'large'`|`'medium'`||
|bordered|是否显示边框|`boolean`|`false`|2.33.0|
|visible **(v-model)**|标签是否可见|`boolean`|`-`||
|default-visible|标签默认是否可见|`boolean`|`true`||
|loading|标签是否为加载中状态|`boolean`|`false`||
|closable|标签是否可关闭|`boolean`|`false`||
|checkable|标签是否可选中|`boolean`|`false`||
|checked **(v-model)**|标签是否选中（标签可选中时可用）|`boolean`|`-`||
|default-checked|标签默认选中状态（标签可选中时可用）|`boolean`|`true`||
|nowrap|标签内容不换行|`boolean`|`false`|2.56.1|
### `<tag>` 事件

|事件名|描述|参数|
|---|---|---|
|close|点击关闭按钮时触发|ev: `MouseEvent`|
|check|用户选中时触发（仅在可选中模式下触发）|checked: `boolean`<br>ev: `MouseEvent`|
### `<tag>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|icon|图标|-|
|close-icon|关闭按钮的图标|-|
