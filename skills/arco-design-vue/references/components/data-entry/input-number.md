---
name: arco-vue-input-number
description: "Arco Design Vue 数字输入框 InputNumber 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-input-number>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 数字输入框 InputNumber

来源组件：上游 `web-vue/components/input-number`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-input-number>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
通过鼠标或者键盘输入范围内的标准数值。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-number v-model="value" :style="{width:'320px'}" placeholder="Please Enter" class="input-demo" :min="10" :max="100"/>
    <a-input-number :style="{width:'320px'}" placeholder="Please Enter" class="input-demo" :min="10" :max="100"/>
    <a-input-number :style="{width:'320px'}" placeholder="Please Enter" :default-value="500" class="input-demo" disabled/>
  </a-space>
</template>

<script>
export default {
  data(){
    return {
      value:15
    }

  }
}
</script>
```

## 示例：按钮模式

### 说明
指定 `mode` 为 `button` 来使用带按钮的数字输入框。




```vue
<template>
  <a-input-number :style="{width:'320px'}" placeholder="Please Enter" :default-value="500" mode="button" class="input-demo" />
</template>
```

## 示例：四种尺寸

### 说明
设置 `size` 可以使用四种尺寸（`mini`, `small`, `medium`, `large`）的数字输入框。高度分别对应`24px`、`28px`、`32px`、`36px`。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-number :style="{width:'320px'}" placeholder="Please Enter" size="large" class="input-demo" />
    <a-input-number :style="{width:'320px'}" placeholder="Please Enter" mode="button" size="large" class="input-demo" />
  </a-space>
</template>
```

## 示例：精度和步长

### 说明
通过 `precision` 来设置数字精度。当 `precision` 小于 `step` 的小数位时，精度取 `step` 的小数个数。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-number :style="{width:'320px'}" placeholder="Please Enter" :default-value="3.6" :step="1.2" :precision="2" class="input-demo" />
    <a-input-number :style="{width:'320px'}" placeholder="Please Enter" :default-value="1.22" :step="1.22" :precision="1" class="input-demo" />
  </a-space>
</template>
```

## 示例：前缀与后缀

### 说明
通过指定 `prefix` 和 `suffix` 插槽来在输入框内添加前缀和后缀。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-number :style="{width:'320px'}" placeholder="Please enter something" allow-clear>
      <template #prefix>
        <icon-user />
      </template>
    </a-input-number>
    <a-input-number :style="{width:'320px'}" placeholder="Please enter something" allow-clear hide-button>
      <template #suffix>
        <icon-info-circle />
      </template>
    </a-input-number>
  </a-space>
</template>
```

## 示例：自定义图标

### 说明
通过指定 `plus` 和 `minus` 插槽来修改数值增减操作的图标。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-input-number :style="{width:'320px'}" placeholder="Please enter something" allow-clear>
       <template #plus>
        <icon-plus />
      </template>
      <template #minus>
        <icon-minus />
      </template>
    </a-input-number>
  </a-space>
</template>
```

## 示例：格式化展示值

### 说明
通过 `formatter` 和 `parser` 配合使用可以定义输入框展示值。




```vue
<template>
  <a-input-number :style="{width:'320px'}" placeholder="Please Enter" class="input-demo" :default-value="12000" :min="0" :formatter="formatter" :parser="parser"/>
</template>

<script>
export default {
  setup(){
    const formatter = (value) => {
      const values = value.split('.');
      values[0]=values[0].replace(/\B(?=(\d{3})+(?!\d))/g, ',');

      return values.join('.')
    };

    const parser = (value) => {
      return value.replace(/,/g, '')
    };

    return {
      formatter,
      parser
    }
  },
}
</script>
```

## 示例：v-model 的触发事件

### 说明
数字输入框默认在 blur 或者按下 Enter 时会修改绑定的值，通过设置属性 model-event="input" 让组件在输入时修改绑定的值。
注意：在此模式下，输入时的值会超出设置的 min/max，组件会在失焦时修正值的大小。




```vue
<template>
  <a-input-number v-model="value" :style="{width:'320px'}" placeholder="Please Enter" class="input-demo" :min="10" :max="100" model-event="input"/>
  <div>value: {{value}}</div>
</template>

<script>
export default {
  data(){
    return {
      value:15
    }

  }
}
</script>
```

## API


### `<input-number>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`number`|`-`||
|default-value|默认值（非受控模式）|`number`|`-`||
|mode|模式（`embed`：按钮内嵌模式，`button`：左右按钮模式）|`'embed' \| 'button'`|`'embed'`||
|precision|数字精度|`number`|`-`||
|step|数字变化步长|`number`|`1`||
|disabled|是否禁用|`boolean`|`false`||
|error|是否为错误状态|`boolean`|`false`||
|max|最大值|`number`|`Infinity`||
|min|最小值|`number`|`-Infinity`||
|formatter|定义输入框展示值|`func`|`-`||
|parser|从 `formatter` 转换为数字，和 `formatter` 搭配使用|`func`|`-`||
|placeholder|输入框提示文字|`string`|`-`||
|hide-button|是否隐藏按钮|`boolean`|`false`||
|size|输入框大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|allow-clear|是否允许清空输入框|`boolean`|`false`||
|model-event|触发 `v-model` 的事件|`'change' \| 'input'`|`'change'`||
|read-only|只读|`boolean`|`false`|2.33.1|
|input-attrs|内部 input 元素的属性|`object`|`-`|2.52.0|
### `<input-number>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|change|值发生改变时触发|value: ` number \| undefined `<br>ev: `Event`||
|focus|输入框获取焦点时触发|ev: `FocusEvent`||
|blur|输入框失去焦点时触发|ev: `FocusEvent`||
|clear|用户点击清除按钮时触发|ev: `Event`|2.23.0|
|input|输入时触发|value: ` number \| undefined `<br>inputValue: `string`<br>ev: `Event`|2.27.0|
|keydown|按下键盘时触发|ev: `MouseEvent`|2.56.0|
### `<input-number>` 方法

|方法名|描述|参数|返回值|
|---|---|---|---|
|focus|使输入框获取焦点|-|-|
|blur|使输入框失去焦点|-|-|
### `<input-number>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|minus|数值减少图标|-|
|plus|数值增加图标|-|
|append|后置标签|-|
|prepend|前置标签|-|
|suffix|后缀|-|
|prefix|前缀|-|
