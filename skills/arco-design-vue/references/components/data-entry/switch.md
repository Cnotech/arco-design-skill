---
name: arco-vue-switch
description: "Arco Design Vue 开关 Switch 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-switch>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 开关 Switch

来源组件：上游 `web-vue/components/switch`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-switch>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
开关的基本用法。




```vue
<template>
  <a-switch />
</template>
```

## 示例：开关类型

### 说明
开关分为 `circle` - **圆形（默认）**、`round` - **圆角**、`line` - **线性**三种类型。




```vue
<template>
  <a-space size="large">
    <a-switch />
    <a-switch type="round"/>
    <a-switch type="line"/>
  </a-space>
</template>
```

## 示例：开关尺寸

### 说明
开关分为 `small`、`medium` 两种尺寸。




```vue
<template>
  <a-space size="large">
    <a-switch />
    <a-switch size="small"/>
  </a-space>
</template>
```

## 示例：禁用状态

### 说明
禁用开关。




```vue
<template>
  <a-space size="large">
    <a-switch disabled/>
    <a-switch :default-checked="true" disabled/>
    <a-switch type="round" disabled/>
    <a-switch :default-checked="true" type="round" disabled/>
    <a-switch type="line" disabled/>
    <a-switch :default-checked="true" type="line" disabled/>
  </a-space>
</template>
```

## 示例：自定义开关的颜色

### 说明
通过 `checked-color` 和 `unchecked-color` 可以自定义开关的颜色。




```vue
<template>
  <a-switch checked-color="#F53F3F" unchecked-color="#14C9C9" />
</template>
```

## 示例：自定义开关的值

### 说明
通过 `checked-value` 和 `unchecked-value` 可以自定义开关的值。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-switch v-model="value" checked-value="yes" unchecked-value="no" />
    <div>Current Value: {{ value }}</div>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref('');

    return {
      value
    }
  },
}
</script>
```

## 示例：切换拦截

### 说明
设置 `beforeChange` 函数，函数的返回值将用于判断是否阻止切换。




```vue
<template>
  <a-space size="large">
    <a-switch :beforeChange="handleChangeIntercept"/>
    <a-switch type="round" :beforeChange="handleChangeIntercept2"/>
    <a-switch type="line" :beforeChange="handleChangeIntercept3"/>
  </a-space>
</template>

<script>
import { Message } from '@arco-design/web-vue';

export default {
  setup() {
    const handleChangeIntercept = async (newValue) => {
      await new Promise((resolve) => setTimeout(resolve, 1000))
      return true
    }

    const handleChangeIntercept2 = async (newValue) => {
      await new Promise((resolve) => setTimeout(resolve, 500))
      if (!newValue) {
        Message.error("OH, You can't change")
        return false
      }
      return true
    }

    const handleChangeIntercept3 = async (newValue) => {
      await new Promise((_, reject) => setTimeout(() => {
        Message.error("OH, Something went wrong")
        reject()
      }, 1000))
      return true
    }

    return {
      handleChangeIntercept,
      handleChangeIntercept2,
      handleChangeIntercept3
    }
  }
}
</script>
```

## 示例：加载中状态

### 说明
通过设置 `loading` 使开关处于加载中状态，此时开关不可点击。




```vue
<template>
  <a-space size="large">
    <a-switch loading />
    <a-switch type="round" loading />
    <a-switch type="line" loading />
  </a-space>
</template>
```

## 示例：自定义文案

### 说明
自定义开关的打开/关闭状态的文字。




```vue
<template>
  <a-space size="large">
    <a-switch>
      <template #checked>
        ON
      </template>
      <template #unchecked>
        OFF
      </template>
    </a-switch>
    <a-switch type="round">
      <template #checked>
        ON
      </template>
      <template #unchecked>
        OFF
      </template>
    </a-switch>
  </a-space>
</template>
```

## 示例：自定义图标

### 说明
自定义开关按钮上显示的图标。




```vue
<template>
  <a-space size="large">
    <a-switch>
      <template #checked-icon>
        <icon-check/>
      </template>
      <template #unchecked-icon>
        <icon-close/>
      </template>
    </a-switch>
    <a-switch type="round">
      <template #checked-icon>
        <icon-check/>
      </template>
      <template #unchecked-icon>
        <icon-close/>
      </template>
    </a-switch>
    <a-switch type="line">
      <template #checked-icon>
        <icon-check/>
      </template>
      <template #unchecked-icon>
        <icon-close/>
      </template>
    </a-switch>
  </a-space>
</template>
```

## API


### `<switch>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`string\|number\|boolean`|`-`||
|default-checked|默认选中状态（非受控状态）|`boolean`|`false`||
|disabled|是否禁用|`boolean`|`false`||
|loading|是否为加载中状态|`boolean`|`false`||
|type|开关的类型|`'circle' \| 'round' \| 'line'`|`'circle'`||
|size|开关的大小|`'small' \| 'medium'`|`'medium'`||
|checked-value|选中时的值|`string\|number\|boolean`|`true`|2.12.0|
|unchecked-value|未选中时的值|`string\|number\|boolean`|`false`|2.12.0|
|checked-color|选中时的开关颜色|`string`|`-`|2.12.0|
|unchecked-color|未选中时的开关颜色|`string`|`-`|2.12.0|
|before-change|switch 状态改变前的钩子， 返回 false 或者返回 Promise 且被 reject 则停止切换。|`(  newValue: string \| number \| boolean) => Promise<boolean \| void> \| boolean \| void`|`-`|2.37.0|
|checked-text|打开状态时的文案（`type='line'`和`size='small'`时不生效）|`string`|`-`|2.45.0|
|unchecked-text|关闭状态时的文案（`type='line'`和`size='small'`时不生效）|`string`|`-`|2.45.0|
### `<switch>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值改变时触发|value: ` boolean \| string \| number `<br>ev: `Event`|
|focus|组件获得焦点时触发|ev: `FocusEvent`|
|blur|组件失去焦点时触发|ev: `FocusEvent`|
### `<switch>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|checked-icon|打开状态时，按钮上的图标|-|
|unchecked-icon|关闭状态时，按钮上的图标|-|
|checked|打开状态时的文案（`type='line'`和`size='small'`时不生效）|-|
|unchecked|关闭状态时的文案（`type='line'`和`size='small'`时不生效）|-|
