---
name: arco-vue-radio
description: "Arco Design Vue 单选框 Radio 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-radio>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 单选框 Radio

来源组件：上游 `web-vue/components/radio`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-radio>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
单选框的基本用法。




```vue
<template>
  <a-space size="large">
    <a-radio value="radio">Radio</a-radio>
    <a-radio value="disabled radio" :default-checked="true" disabled>Disabled Radio</a-radio>
  </a-space>
</template>
```

## 示例：受控

### 说明
通过 `v-model` (`model-value`) 属性控制是否选中




```vue
<template>
  <a-space size="large">
    <a-radio v-model="checked1">v-model</a-radio>
    <a-radio :model-value="true">binding "true"</a-radio>
    <a-radio :model-value="checked2">binding value2</a-radio>
    <a-radio :default-checked="true">uncontrolled state</a-radio>
  </a-space>
  <div :style="{ marginTop: '20px' }">
    <a-space size="large">
      <a-button type="primary" @click="handleSetCheck">
        {{ checked2 ? 'uncheck' : 'check' }} value2
      </a-button>
      <a-button @click="handleReset"> reset all </a-button>
    </a-space>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const checked1 = ref(false);
    const checked2 = ref(false);

    const handleSetCheck = () => {
      checked2.value = !checked2.value;
    };

    const handleReset = () => {
      checked1.value = false;
      checked2.value = false;
    };

    return {
      checked1,
      checked2,
      handleSetCheck,
      handleReset,
    };
  },
};
</script>
```

## 示例：单选框组

### 说明
通过 `<a-radio-group>` 组件展示单选框组。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-radio-group>
      <a-radio value="A">A</a-radio>
      <a-radio value="B">B</a-radio>
      <a-radio value="C">C</a-radio>
      <a-radio value="D">D</a-radio>
    </a-radio-group>
    <a-radio-group>
      <a-radio value="A">A</a-radio>
      <a-radio value="B">B</a-radio>
      <a-radio value="C">C</a-radio>
      <a-radio value="D" disabled>D</a-radio>
    </a-radio-group>
  </a-space>
</template>
```

## 示例：单选框组选项

### 说明
`a-radio-group` 通过 `options` 属性设置子元素




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-radio-group v-model="value1" :options="plainOptions" />
    <a-radio-group v-model="value2" :options="options" />
    <a-radio-group v-model="value2" :options="options">
      <template #label="{ data }">
        <a-tag>{{ data.label }}</a-tag>
      </template>
    </a-radio-group>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value1 = ref('plain 1');
    const plainOptions = ['plain 1', 'plain 2', 'plain 3'];

    const value2 = ref('1');
    const options = [
      { label: 'option 1', value: '1' },
      { label: 'option 2', value: '2' },
      { label: 'option 3', value: '3', disabled: true },
    ];

    return {
      plainOptions,
      options,
      value1,
      value2,
    };
  },
};
</script>
```

## 示例：单选框组方向

### 说明
通过设置 `direction="vertical"` 可以展示竖直的单选框组。




```vue
<template>
  <a-radio-group direction="vertical">
    <a-radio value="A">A</a-radio>
    <a-radio value="B">B</a-radio>
    <a-radio value="C">C</a-radio>
    <a-radio value="D">D</a-radio>
  </a-radio-group>
</template>
```

## 示例：按钮类型的单选框组

### 说明
通过指定 `type="button"` ，可以显示按钮类型的单选框组。




```vue
<template>
  <a-radio-group type="button">
    <a-radio value="Beijing">Beijing</a-radio>
    <a-radio value="Shanghai">Shanghai</a-radio>
    <a-radio value="Guangzhou">Guangzhou</a-radio>
    <a-radio value="Shenzhen">Shenzhen</a-radio>
  </a-radio-group>
</template>
```

## 示例：按钮类型单选框组的尺寸

### 说明
按钮类型的单选框组分为 `mini`、`small`、`medium`、`large` 四种尺寸。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-radio-group type="button" size="mini">
      <a-radio value="Beijing">Beijing</a-radio>
      <a-radio value="Shanghai">Shanghai</a-radio>
      <a-radio value="Guangzhou">Guangzhou</a-radio>
      <a-radio value="Shenzhen">Shenzhen</a-radio>
    </a-radio-group>
    <a-radio-group type="button" size="small">
      <a-radio value="Beijing">Beijing</a-radio>
      <a-radio value="Shanghai">Shanghai</a-radio>
      <a-radio value="Guangzhou">Guangzhou</a-radio>
      <a-radio value="Shenzhen">Shenzhen</a-radio>
    </a-radio-group>
    <a-radio-group type="button">
      <a-radio value="Beijing">Beijing</a-radio>
      <a-radio value="Shanghai">Shanghai</a-radio>
      <a-radio value="Guangzhou">Guangzhou</a-radio>
      <a-radio value="Shenzhen">Shenzhen</a-radio>
    </a-radio-group>
    <a-radio-group type="button" size="large">
      <a-radio value="Beijing">Beijing</a-radio>
      <a-radio value="Shanghai">Shanghai</a-radio>
      <a-radio value="Guangzhou">Guangzhou</a-radio>
      <a-radio value="Shenzhen">Shenzhen</a-radio>
    </a-radio-group>
  </a-space>
</template>
```

## 示例：布局

### 说明
使用 `<a-radio-group>` 传入 `<a-radio>`，配合 `<a-grid>` 组件实现灵活的布局。




```vue
<template>
  <a-radio-group v-model="checkedValue">
    <a-grid :cols="3" :colGap="24" :rowGap="16">
      <a-grid-item>
        <a-radio value="1">Option 1</a-radio>
      </a-grid-item>
      <a-grid-item>
        <a-radio value="2" disabled>Option 2</a-radio>
      </a-grid-item>
      <a-grid-item>
        <a-radio value="3">Option 3</a-radio>
      </a-grid-item>
      <a-grid-item>
        <a-radio value="4">Option 4</a-radio>
      </a-grid-item>
      <a-grid-item>
        <a-radio value="5">Option 5</a-radio>
      </a-grid-item>
    </a-grid>
  </a-radio-group>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const checkedValue = ref('1');

    return {
      checkedValue,
    };
  },
};
</script>
```

## 示例：自定义单选框

### 说明
使用 #radio 插槽自定义复选框的展示




```vue
<template>
  <a-radio-group default-value="1">
    <a-radio value="1">
      <template #radio="{ checked }">
        <a-tag :checked="checked" checkable>This is a tag radio 1</a-tag>
      </template>
    </a-radio>
    <a-radio value="2">
      <template #radio="{ checked }">
        <a-tag :checked="checked" checkable>This is a tag radio 2</a-tag>
      </template>
    </a-radio>
    <a-radio value="3">
      <template #radio="{ checked }">
        <a-tag :checked="checked" checkable>This is a tag radio 3</a-tag>
      </template>
    </a-radio>
  </a-radio-group>

  <div :style="{ marginTop: '20px' }">
    <a-radio-group>
      <template v-for="item in 2" :key="item">
        <a-radio :value="item">
          <template #radio="{ checked }">
            <a-space
              align="start"
              class="custom-radio-card"
              :class="{ 'custom-radio-card-checked': checked }"
            >
              <div className="custom-radio-card-mask">
                <div className="custom-radio-card-mask-dot" />
              </div>
              <div>
                <div className="custom-radio-card-title">
                  radio Card {{ item }}
                </div>
                <a-typography-text type="secondary">
                  this is a text
                </a-typography-text>
              </div>
            </a-space>
          </template>
        </a-radio>
      </template>
    </a-radio-group>
  </div>
</template>

<style scoped>
.custom-radio-card {
  padding: 10px 16px;
  border: 1px solid var(--color-border-2);
  border-radius: 4px;
  width: 250px;
  box-sizing: border-box;
}

.custom-radio-card-mask {
  height: 14px;
  width: 14px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 100%;
  border: 1px solid var(--color-border-2);
  box-sizing: border-box;
}

.custom-radio-card-mask-dot {
  width: 8px;
  height: 8px;
  border-radius: 100%;
}

.custom-radio-card-title {
  color: var(--color-text-1);
  font-size: 14px;
  font-weight: bold;
  margin-bottom: 8px;
}

.custom-radio-card:hover,
.custom-radio-card-checked,
.custom-radio-card:hover .custom-radio-card-mask,
.custom-radio-card-checked  .custom-radio-card-mask{
  border-color: rgb(var(--primary-6));
}

.custom-radio-card-checked {
  background-color: var(--color-primary-light-1);
}

.custom-radio-card:hover .custom-radio-card-title,
.custom-radio-card-checked .custom-radio-card-title {
  color: rgb(var(--primary-6));
}

.custom-radio-card-checked .custom-radio-card-mask-dot {
  background-color: rgb(var(--primary-6));
}
</style>
```

## API


### `<radio>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|model-value **(v-model)**|绑定值|`string \| number \| boolean`|`-`|
|default-checked|默认是否选中（非受控状态）|`boolean`|`false`|
|value|选项的 `value`|`string \| number \| boolean`|`true`|
|type|单选的类型|`'radio' \| 'button'`|`'radio'`|
|disabled|是否禁用|`boolean`|`false`|
### `<radio>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值改变时触发|value: ` string \| number \| boolean `<br>ev: `Event`|
### `<radio>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|radio|自定义单选框|checked: `boolean`<br>disabled: `boolean`|2.18.0|




### `<radio-group>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`string \| number \| boolean`|`-`||
|default-value|默认值（非受控状态）|`string \| number \| boolean`|`''`||
|type|单选框组的类型|`'radio' \| 'button'`|`'radio'`||
|size|单选框组的尺寸|`'mini' \| 'small' \| 'medium' \| 'large'`|`-`||
|options|选项|`Array<string \| number \| RadioOption>`|`-`|2.27.0|
|direction|单选框组的方向|`'horizontal' \| 'vertical'`|`'horizontal'`||
|disabled|是否禁用|`boolean`|`false`||
### `<radio-group>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值改变时触发|value: ` string \| number \| boolean `|
### `<radio-group>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|radio|自定义单选框|checked: `boolean`<br>disabled: `boolean`|2.27.0|
|label|radio 文案内容|data: `RadioOption`|2.27.0|




### RadioOption

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|label|文案|`RenderContent`|`-`|
|value|选项的 `value`|`string \| number`|`-`|
|disabled|是否禁用|`boolean`|`false`|
