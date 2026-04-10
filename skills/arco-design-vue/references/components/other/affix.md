---
name: arco-vue-affix
description: "Arco Design Vue 固钉 Affix 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-affix>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 固钉 Affix

来源组件：上游 `web-vue/components/affix`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-affix>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
基本用法，不设置固定位置时，当页面滚动元素不可见时，元素固定在页面最顶部。




```vue
<template>
  <a-affix>
    <a-button type="primary">Affix Top</a-button>
  </a-affix>
</template>
```

## 示例：顶部固定

### 说明
当页面滚动或浏览器窗口改变时，元素向上滚动到距顶部一定距离时固定。




```vue
<template>
  <a-affix :offsetTop="80">
    <a-button type="primary">80px to affix top</a-button>
  </a-affix>
</template>
```

## 示例：底部固定

### 说明
当页面滚动或浏览器窗口改变时，元素向下滚动到距底部一定距离时固定。




```vue
<template>
  <a-affix :offsetBottom="120">
    <a-button type="primary">120px to affix bottom</a-button>
  </a-affix>
</template>
```

## 示例：固定状态改变回调

### 说明
当固定状态发生改变时，会触发事件。




```vue
<template>
  <a-affix
    :offsetBottom="80"
    @change="onChange"
  >
    <a-button type="primary">80px to affix bottom</a-button>
  </a-affix>
</template>
<script>
import { defineComponent } from 'vue';

export default defineComponent({
  setup() {
    const onChange = (fixed) => {
      console.log(`${fixed}`);
    };
    return {
      onChange
    };
  }
});
</script>
```

## 示例：滚动容器

### 说明
用 `target` 设置需要监听其滚动事件的元素，默认为 window。

`target` 指定为非 window 容器时，可能会出现 `target`外层元素滚动，固钉元素跑出滚动容器的问题。这个时候可以通过传入`targetContainer`传入`target`外层的滚动元素。`Affix`
会监听该元素的滚动事件来实时更新滚钉元素的位置。 当然您也可以在业务代码中自己监听target外层滚动元素的 `scroll` 事件，并调用 `updatePosition` 去更新固钉的位置。




```vue

<template>
  <div
    style="height: 200px; overflow: auto"
    ref="containerRef"
  >
    <div style="height: 400px; background: #cccccc; overflow: hidden">
      <a-affix
        :offsetTop="20"
        :target="containerRef"
        style="margin: 40px"
      >
        <a-button type="primary">Affix in scrolling container</a-button>
      </a-affix>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const containerRef = ref();

    return {
      containerRef,
    };
  },
}
</script>
```

## API


### `<affix>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|offset-top|距离窗口顶部达到指定偏移量后触发|`number`|`0`|
|offset-bottom|距离窗口底部达到指定偏移量后触发|`number`|`-`|
|target|滚动容器，默认是 `window`|`string \| HTMLElement \| Window`|`-`|
|target-container|`target`的外层滚动元素，默认是 `window`。`Affix `将会监听该元素的滚动事件，并实时更新固钉的位置。主要是为了解决 `target` 属性指定为非 `window` 元素时，如果外层元素滚动，可能会导致固钉跑出容器问题|`string \| HTMLElement \| Window`|`-`|
### `<affix>` 事件

|事件名|描述|参数|
|---|---|---|
|change|固定状态发生改变时触发|fixed: `boolean`|
### `<affix>` 方法

|方法名|描述|参数|返回值|
|---|---|---|---|
|updatePosition|更新位置|-|-|
