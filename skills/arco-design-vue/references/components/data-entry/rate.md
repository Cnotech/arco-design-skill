---
name: arco-vue-rate
description: "Arco Design Vue 评分 Rate 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-rate>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 评分 Rate

来源组件：上游 `web-vue/components/rate`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-rate>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
评分组件基本用法。




```vue
<template>
  <a-rate/>
</template>
```

## 示例：半选

### 说明
指定 `allow-half` 来开启半选。




```vue
<template>
  <a-rate :default-value="2.5" allow-half/>
</template>
```

## 示例：自定义颜色

### 说明
通过 color 可以自定义颜色。另外可以通过对象形式自定义不同分值时的颜色。




```vue
<template>
  <a-space direction="vertical">
    <a-rate color="red" />
    <a-rate :color="color" />
  </a-space>
</template>

<script>
export default {
  setup() {
    const color = {
      2: 'red',
      4: 'green',
      5: 'blue'
    }
    return {
      color
    }
  },
}
</script>
```

## 示例：只读模式

### 说明
通过设置 `readonly` 属性让评分组件为只读状态。




```vue
<template>
  <a-rate :default-value="4" readonly />
</template>
```

## 示例：支持清除

### 说明
通过设置 `allow-clear` 来允许清除评分。




```vue
<template>
  <a-rate :default-value="3" allow-clear/>
</template>
```

## 示例：自定义评分字符

### 说明
可以将星星替换为其他字符，比如表情、字母，数字，字体图标甚至中文。




```vue
<template>
  <a-rate :default-value="2">
    <template #character="{ index }">
      <icon-check v-if="index < 3"/>
      <icon-close v-else/>
    </template>
  </a-rate>
</template>
```

## 示例：任意长度的评分

### 说明
通过指定 `count` 来指定任意长度的评分组件。




```vue
<template>
  <a-rate :count="10"/>
</template>
```

## 示例：笑脸分级

### 说明
通过 `grading` 使用笑脸分级。




```vue
<template>
  <a-rate grading/>
</template>
```

## API


### `<rate>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|count|评分的总数|`number`|`5`||
|model-value **(v-model)**|绑定值|`number`|`-`||
|default-value|默认值|`number`|`0`||
|allow-half|是否允许半选|`boolean`|`false`||
|allow-clear|是否允许清除|`boolean`|`false`||
|grading|是否开启笑脸分级|`boolean`|`false`||
|readonly|是否为只读状态|`boolean`|`false`||
|disabled|是否禁用|`boolean`|`false`||
|color|颜色|`string \| Record<string, string>`|`-`|2.18.0|
### `<rate>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值改变时触发|value: `number`|
|hover-change|鼠标移动到数值上时触发|value: `number`|
### `<rate>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|character|符号|index: `number`|
