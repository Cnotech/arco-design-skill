---
name: arco-vue-checkbox
description: "Arco Design Vue 复选框 Checkbox 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-checkbox>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 复选框 Checkbox

来源组件：上游 `web-vue/components/checkbox`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-checkbox>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
复选框的基本用法。




```vue
<template>
  <a-checkbox value="1">Option 1</a-checkbox>
</template>
```

## 示例：受控

### 说明
通过 `v-model` (`model-value`) 属性控制是否选中




```vue
<template>
  <a-space size="large">
    <a-checkbox v-model="checked1">v-model</a-checkbox>
    <a-checkbox :model-value="true">binding value</a-checkbox>
    <a-checkbox :model-value="checked2">binding value2</a-checkbox>
    <a-checkbox :default-checked="true">uncontrolled state</a-checkbox>
  </a-space>
  <div :style="{ marginTop: '20px' }">
    <a-button type="primary" @click="handleSetCheck">
      {{ checked2 ? 'uncheck' : 'check' }} value2
    </a-button>
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

    return {
      checked1,
      checked2,
      handleSetCheck,
    };
  },
};
</script>
```

## 示例：禁用状态

### 说明
禁用复选框。




```vue
<template>
  <a-space size="large">
    <a-checkbox value="1" disabled>Disabled Option 1</a-checkbox>
    <a-checkbox :default-checked="true" disabled>Disabled Option 2</a-checkbox>
  </a-space>
</template>
```

## 示例：复选框组

### 说明
通过 `<a-checkbox-group>` 组件展示复选框组。设置 `direction="vertical"` 可以展示竖向的复选框组。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-checkbox-group :default-value="['1']">
      <a-checkbox value="1">Option 1</a-checkbox>
      <a-checkbox value="2">Option 2</a-checkbox>
      <a-checkbox value="3">Option 3</a-checkbox>
    </a-checkbox-group>
    <a-checkbox-group direction="vertical">
      <a-checkbox value="1">Option 1</a-checkbox>
      <a-checkbox value="2">Option 2</a-checkbox>
      <a-checkbox value="3">Option 3</a-checkbox>
    </a-checkbox-group>
  </a-space>
</template>
```

## 示例：复选框组选项

### 说明
`a-checkbox-group` 通过 `options` 属性设置子元素




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-checkbox-group v-model="value1" :options="plainOptions" />
    <a-checkbox-group v-model="value2" :options="options" />
    <a-checkbox-group v-model="value2" :options="options">
      <template #label="{ data }">
        <a-tag>{{ data.label }}</a-tag>
      </template>
    </a-checkbox-group>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value1 = ref(['Plain 1']);
    const plainOptions = ['Plain 1', 'Plain 2', 'Plain 3'];

    const value2 = ref(['1']);
    const options = [
      { label: 'Option 1', value: '1' },
      { label: 'Option 2', value: '2' },
      { label: 'Option 3', value: '3', disabled: true },
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

## 示例：限制可勾选数量

### 说明
通过设置 `max` 限制最多可被勾选的项目数。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-checkbox-group :max="2" v-model="value1" :options="plainOptions" />
    <a-checkbox-group :max="2" :default-value="['1']">
      <a-checkbox value="1" disabled>Option 1</a-checkbox>
      <a-checkbox value="2">Option 2</a-checkbox>
      <a-checkbox value="3">Option 3</a-checkbox>
      <a-checkbox value="4">Option 4</a-checkbox>
    </a-checkbox-group>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value1 = ref(['Plain 1']);
    const plainOptions = ['Plain 1', 'Plain 2', 'Plain 3', 'Plain 4'];

    return {
      plainOptions,
      value1,
    };
  },
};
</script>
```

## 示例：全选

### 说明
在实现全选的功能时，可以通过 `indeterminate` 属性展示半选效果。




```vue
<template>
  <a-space direction="vertical">
    <a-checkbox :model-value="checkedAll" :indeterminate="indeterminate" @change="handleChangeAll">Check All
    </a-checkbox>
    <a-checkbox-group v-model="data" @change="handleChange">
      <a-checkbox value="1">Option 1</a-checkbox>
      <a-checkbox value="2">Option 2</a-checkbox>
      <a-checkbox value="3">Option 3</a-checkbox>
    </a-checkbox-group>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const indeterminate = ref(false)
    const checkedAll = ref(false)
    const data = ref([])

    const handleChangeAll = (value) => {
      indeterminate.value = false;
      if (value) {
        checkedAll.value = true;
        data.value = ['1', '2', '3']
      } else {
        checkedAll.value = false;
        data.value = []
      }
    }

    const handleChange = (values) => {
      if (values.length === 3) {
        checkedAll.value = true
        indeterminate.value = false;
      } else if (values.length === 0) {
        checkedAll.value = false
        indeterminate.value = false;
      } else {
        checkedAll.value = false
        indeterminate.value = true;
      }
    }

    return {
      indeterminate,
      checkedAll,
      data,
      handleChangeAll,
      handleChange
    }
  },
}
</script>
```

## 示例：布局

### 说明
使用 `<a-checkbox-group>` 传入 `<a-checkbox>`，配合 `<a-grid>` 组件实现灵活的布局。




```vue
<template>
  <a-checkbox-group v-model="checkedValue">
    <a-grid :cols="3" :colGap="24" :rowGap="16">
      <a-grid-item>
        <a-checkbox value="1">Option 1</a-checkbox>
      </a-grid-item>
      <a-grid-item>
        <a-checkbox value="2" disabled>Option 2</a-checkbox>
      </a-grid-item>
      <a-grid-item>
        <a-checkbox value="3">Option 3</a-checkbox>
      </a-grid-item>
      <a-grid-item>
        <a-checkbox value="4">Option 4</a-checkbox>
      </a-grid-item>
      <a-grid-item>
        <a-checkbox value="5">Option 5</a-checkbox>
      </a-grid-item>
    </a-grid>
  </a-checkbox-group>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const checkedValue = ref(['1', '2']);

    return {
      checkedValue,
    };
  },
};
</script>
```

## 示例：自定义复选框

### 说明
使用 #checkbox 插槽自定义复选框的展示




```vue
<template>
  <a-checkbox-group :default-value="['1']">
    <a-checkbox value="1">
      <template #checkbox="{ checked }">
        <a-tag :checked="checked" checkable>This is a tag checkbox 1</a-tag>
      </template>
    </a-checkbox>
    <a-checkbox value="2">
      <template #checkbox="{ checked }">
        <a-tag :checked="checked" checkable>This is a tag checkbox 2</a-tag>
      </template>
    </a-checkbox>
    <a-checkbox value="3">
      <template #checkbox="{ checked }">
        <a-tag :checked="checked" checkable>This is a tag checkbox 3</a-tag>
      </template>
    </a-checkbox>
  </a-checkbox-group>

  <div :style="{ marginTop: '20px' }">
    <a-checkbox-group :default-value="[1]">
      <template v-for="item in 2" :key="item">
        <a-checkbox :value="item">
          <template #checkbox="{ checked }">
            <a-space
              align="start"
              class="custom-checkbox-card"
              :class="{ 'custom-checkbox-card-checked': checked }"
            >
              <div className="custom-checkbox-card-mask">
                <div className="custom-checkbox-card-mask-dot" />
              </div>
              <div>
                <div className="custom-checkbox-card-title">
                  Checkbox Card {{ item }}
                </div>
                <a-typography-text type="secondary">
                  this is a text
                </a-typography-text>
              </div>
            </a-space>
          </template>
        </a-checkbox>
      </template>
    </a-checkbox-group>
  </div>
</template>

<style scoped>
.custom-checkbox-card {
  padding: 10px 16px;
  border: 1px solid var(--color-border-2);
  border-radius: 4px;
  width: 250px;
  box-sizing: border-box;
}

.custom-checkbox-card-mask {
  height: 14px;
  width: 14px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 2px;
  border: 1px solid var(--color-border-2);
  box-sizing: border-box;
}

.custom-checkbox-card-mask-dot {
  width: 8px;
  height: 8px;
  border-radius: 2px;
}

.custom-checkbox-card-title {
  color: var(--color-text-1);
  font-size: 14px;
  font-weight: bold;
  margin-bottom: 8px;
}

.custom-checkbox-card:hover,
.custom-checkbox-card-checked,
.custom-checkbox-card:hover .custom-checkbox-card-mask,
.custom-checkbox-card-checked .custom-checkbox-card-mask {
  border-color: rgb(var(--primary-6));
}

.custom-checkbox-card-checked {
  background-color: var(--color-primary-light-1);
}

.custom-checkbox-card:hover .custom-checkbox-card-title,
.custom-checkbox-card-checked .custom-checkbox-card-title {
  color: rgb(var(--primary-6));
}

.custom-checkbox-card-checked .custom-checkbox-card-mask-dot {
  background-color: rgb(var(--primary-6));
}
</style>
```

## API


### `<checkbox>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|model-value **(v-model)**|绑定值|`boolean \| Array<string \| number \| boolean>`|`-`|
|default-checked|默认是否选中（非受控状态）|`boolean`|`false`|
|value|选项的 `value`|`string\|number\|boolean`|`-`|
|disabled|是否禁用|`boolean`|`false`|
|indeterminate|是否为半选状态|`boolean`|`false`|
### `<checkbox>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值改变时触发|value: ` boolean \| (string \| number \| boolean)[] `<br>ev: `Event`|
### `<checkbox>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|checkbox|自定义复选框|checked: `boolean`<br>disabled: `boolean`|2.18.0|




### `<checkbox-group>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`Array<string \| number \| boolean>`|`-`||
|default-value|默认值（非受控状态）|`Array<string \| number \| boolean>`|`[]`||
|max|支持最多选中的数量|`number`|`-`|2.36.0|
|options|选项|`Array<string \| number \| CheckboxOption>`|`-`|2.27.0|
|direction|复选框的排列方向|`Direction`|`'horizontal'`||
|disabled|是否禁用|`boolean`|`false`||
### `<checkbox-group>` 事件

|事件名|描述|参数|
|---|---|---|
|change|值改变时触发|value: `(string \| number \| boolean)[]`<br>ev: `Event`|
### `<checkbox-group>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|checkbox|自定义复选框|checked: `boolean`<br>disabled: `boolean`|2.27.0|
|label|checkbox 文案内容|data: `CheckboxOption`|2.27.0|




### CheckboxOption

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|label|文案|`RenderContent`|`-`|
|value|选项的 `value`|`string \| number`|`-`|
|disabled|是否禁用|`boolean`|`false`|
|indeterminate|是否为半选状态|`boolean`|`false`|
