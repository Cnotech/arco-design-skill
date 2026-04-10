---
name: arco-vue-slider
description: "Arco Design Vue 滑动输入条 Slider 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-slider>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 滑动输入条 Slider

来源组件：上游 `web-vue/components/slider`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-slider>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
滑动输入条的基本用法。




```vue
<template>
  <a-slider :default-value="50" :style="{ width: '200px' }" />
</template>
```

## 示例：禁用状态

### 说明
禁用滑动输入条。




```vue
<template>
  <a-slider :default-value="50" :style="{ width: '200px' }" disabled/>
</template>
```

## 示例：设置步长

### 说明
通过 `step` 设置步长，默认步长为 1。建议设置能够被 `max-min` 整除的值，否则会出现可选最大值小于 `max` 的情况。当设置 `show-ticks` 时，显示步长刻度线。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-form :model="data" layout="inline">
      <a-form-item label="Step" field="step">
        <a-input-number :style="{ width: '100px' }" v-model="data.step" />
      </a-form-item>
      <a-form-item label="Show steps" field="showTicks">
        <a-switch v-model="data.showTicks" />
      </a-form-item>
    </a-form>
    <a-slider :default-value="20" :style="{ width: '300px' }" :step="data.step" :show-ticks="data.showTicks" />
  </a-space>
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const data = reactive({
      step: 5,
      showTicks: true
    });

    return {
      data
    }
  },
}
</script>
```

## 示例：添加文本标签

### 说明
通过设置 `marks` 可以添加文本标签。




```vue
<template>
  <a-slider :default-value="5" :style="{ width: '300px' }" :max="15" :marks="marks" />
</template>

<script>
export default {
  setup() {
    const marks = {
      0: '0km',
      5: '5km',
      10: '10km',
      15: '15km'
    };
    return {
      marks
    }
  },
}
</script>
```

## 示例：范围选择

### 说明
通过设置 `range` 可开启范围选择，此时 `modelValue` 为数组。




```vue
<template>
  <a-slider v-model="value" :style="{ width: '300px' }" range />
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref([5, 10]);

    return {
      value
    }

  }
}
</script>
```

## 示例：显示输入框

### 说明
当设置 `show-input` 时，将显示输入框。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-slider :default-value="10" :style="{ width: '300px' }" show-input />
    <a-slider :default-value="[10,20]" :style="{ width: '380px' }" range show-input />
  </a-space>
</template>
```

## 示例：竖直滑动条

### 说明
设置 `direction="vertical"` ，将会显示竖直的滑动条。




```vue
<template>
  <a-space align="start">
    <a-slider
      :default-value="50"
      direction="vertical"
    />

    <a-slider
      direction="vertical"
      :default-value="5"
      :style="{ width: '300px' }"
      :max="15"
      :marks="{
        5: '5km',
        10: '10km',
      }"
    />
  </a-space>
</template>
```

## 示例：自定义提示

### 说明
通过设置 `format-tooltip` 可以自定义提示文字。




```vue
<template>
  <a-slider :min="0" :max="50" :style="{ width: '200px' }" :format-tooltip="formatter" />
</template>

<script>
export default {
  setup() {
    const formatter = (value) => {
      return `${Math.round((value / 50) * 100)}%`
    };

    return {
      formatter
    }
  },
}
</script>
```

## API


### `<slider>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`number \| [number, number]`|`-`||
|default-value|默认值（非受控状态）|`number \| [number, number]`|`0`||
|step|滑动的步长|`number`|`1`||
|min|滑动范围的最小值|`number`|`0`||
|marks|设置显示的标签|`Record<number, string>`|`-`||
|max|滑动范围的最大值|`number`|`100`||
|direction|滑动输入条的方向|`Direction`|`'horizontal'`||
|disabled|是否禁用|`boolean`|`false`||
|show-ticks|是否显示刻度线|`boolean`|`false`||
|show-input|是否显示输入框|`boolean`|`false`||
|range|是否开启范围选择|`boolean`|`false`||
|show-tooltip|是否显示tooltip|`boolean`|`true`|2.42.0|
### `<slider>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值改变时触发|value: `number \| [number, number]`|
