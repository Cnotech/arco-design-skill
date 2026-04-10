---
name: arco-vue-overflow-list
description: "Arco Design Vue 折叠列表 OverflowList 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-overflow-list>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 折叠列表 OverflowList

来源组件：上游 `web-vue/components/overflow-list`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-overflow-list>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
折叠列表的基本使用方法。




```vue
<template>
  <a-form auto-label-width>
    <a-form-item label="Tag Number">
      <a-input-number v-model="number" :min="0" :max="20" style="width: 200px"/>
    </a-form-item>
    <a-form-item label="List Width">
      <a-slider v-model="width" :min="0" :max="800" />
    </a-form-item>
  </a-form>
  <div :style="{width:`${width}px`,marginTop:'20px'}">
    <a-overflow-list>
      <div>DIV Element</div>
      <a-tag v-for="item of tags" :key="item">Tag{{item}}</a-tag>
    </a-overflow-list>
  </div>
</template>

<script>
import { computed, ref } from 'vue';

export default {
  setup() {
    const width = ref(500);
    const number = ref(10);
    const tags = computed(() => Array.from({length: number.value}, (_, idx) => idx + 1));

    return {
      width,
      number,
      tags
    }
  }
}
</script>
```

## 示例：折叠方向

### 说明
通过 `from` 属性可以设置折叠的方向。




```vue
<template>
  <a-form auto-label-width>
    <a-form-item label="Tag Number">
      <a-input-number v-model="number" :min="0" :max="20" style="width: 200px"/>
    </a-form-item>
    <a-form-item label="List Width">
      <a-slider v-model="width" :min="0" :max="800" />
    </a-form-item>
  </a-form>
  <div :style="{width:`${width}px`,marginTop:'20px'}">
    <a-overflow-list from="start">
      <div>DIV Element</div>
      <a-tag v-for="item of tags" :key="item">Tag{{item}}</a-tag>
    </a-overflow-list>
  </div>
</template>

<script>
import { computed, ref } from 'vue';

export default {
  setup() {
    const width = ref(500);
    const number = ref(10);
    const tags = computed(() => Array.from({length: number.value}, (_, idx) => idx + 1));

    return {
      width,
      number,
      tags
    }
  }
}
</script>
```

## API


### `<overflow-list>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|min|最少展示的元素个数|`number`|`0`|
|margin|项目间隔|`number`|`8`|
|from|折叠方向|`'start' \| 'end'`|`'end'`|
### `<overflow-list>` 事件

|事件名|描述|参数|
|---|---|---|
|change|溢出数量改变时触发|value: `number`|
### `<overflow-list>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|overflow|折叠元素|number: `number`|
