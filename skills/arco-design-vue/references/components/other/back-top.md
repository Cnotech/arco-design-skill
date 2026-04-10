---
name: arco-vue-back-top
description: "Arco Design Vue 返回顶部 BackTop 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-back-top>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 返回顶部 BackTop

来源组件：上游 `web-vue/components/back-top`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-back-top>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
当容器滚动到一定高度的时候，在右下角会出现一个返回顶部的按钮。




```vue
<template>
  <div class="wrapper">
    <ul id="basic-demo">
      <li v-for="(_, index) of Array(40)" :key="index">This is the content</li>
    </ul>
    <a-back-top target-container="#basic-demo" :style="{position:'absolute'}" />
  </div>
</template>

<style scoped lang="less">
.wrapper {
  position: relative;

  ul {
    height: 200px;
    overflow-y: auto;

    li {
      line-height: 30px;
    }
  }
}
</style>
```

## 示例：自定义按钮

### 说明
可以自定义返回按钮。




```vue
<template>
  <div class="wrapper">
    <ul id="custom-demo">
      <li v-for="(_, index) of Array(40)" :key="index">This is the content</li>
    </ul>
    <a-back-top target-container="#custom-demo" :style="{position:'absolute'}" >
      <a-button>UP</a-button>
    </a-back-top>
  </div>
</template>

<style scoped lang="less">
.wrapper {
  position: relative;

  ul {
    height: 200px;
    overflow-y: auto;

    li {
      line-height: 30px;
    }
  }
}
</style>
```

## API


### `<back-top>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|visible-height|显示回到顶部按钮的触发滚动高度|`number`|`200`|
|target-container|滚动事件的监听容器|`string \| HTMLElement`|`-`|
|easing|滚动动画的缓动方式，可选值参考 [BTween](https://github.com/PengJiyuan/b-tween)|`string`|`'quartOut'`|
|duration|滚动动画的持续时间|`number`|`200`|
