---
name: arco-vue-transfer
description: "Arco Design Vue 数据穿梭框 Transfer 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-transfer>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 数据穿梭框 Transfer

来源组件：上游 `web-vue/components/transfer`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-transfer>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
数据穿梭框的基本用法。




```vue
<template>
  <a-transfer :data="data" :default-value="value" />
</template>

<script>
export default {
  setup() {
    const data = Array(8).fill(undefined).map((_, index) => ({
      value: `option${index + 1}`,
      label: `Option ${index + 1}`
    }));
    const value = ['option1', 'option3', 'option5'];

    return {
      data,
      value
    }
  },
}
</script>
```

## 示例：搜索

### 说明
通过设置 `show-search` 来使用带搜索框的穿梭框，可以自定义搜索函数。




```vue
<template>
  <a-transfer
    show-search
    :data="data"
    :default-value="value"
    :source-input-search-props="{
      placeholder:'source item search'
    }"
    :target-input-search-props="{
      placeholder:'target item search'
    }"
  />
</template>

<script>
export default {
  setup() {
    const data = Array(8).fill(undefined).map((_, index) => ({
      value: `option${index + 1}`,
      label: `Option ${index + 1}`
    }));
    const value = ['option1', 'option3', 'option5'];

    return {
      data,
      value
    }
  },
}
</script>
```

## 示例：单向

### 说明
通过设置 `one-way` ，使用单向模式的穿梭框。




```vue
<template>
  <a-transfer :data="data" :default-value="value" one-way/>
</template>

<script>
export default {
  setup() {
    const data = Array(8).fill(undefined).map((_, index) => ({
      value: `option${index + 1}`,
      label: `Option ${index + 1}`
    }));
    const value = ['option1', 'option3', 'option5'];

    return {
      data,
      value
    }
  },
}
</script>
```

## 示例：自定义选项渲染

### 说明
通过 `item` 插槽自定义选项的渲染内容。




```vue

<template>
  <a-transfer :data="data" :default-value="value">
    <template #item="{ label }">
      <icon-up />
      {{ label }}
    </template>
  </a-transfer>
</template>

<script>
export default {
  setup() {
    const data = Array(8).fill(undefined).map((_, index) => {
      return {
        value: `option${index + 1}`,
        label: `Option ${index + 1}`,
        disabled: index === 1
      }
    });
    const value = ['option1', 'option3', 'option5'];

    return {
      data,
      value
    }
  },
}
</script>
```

## 示例：简单模式

### 说明
通过设置 `simple` 来开启简单模式，点击选项即可移动。




```vue
<template>
  <a-transfer :data="data" :default-value="value" simple />
</template>

<script>
export default {
  setup() {
    const data = Array(8).fill(undefined).map((_, index) => ({
      value: `option${index + 1}`,
      label: `Option ${index + 1}`
    }));
    const value = ['option1', 'option3', 'option5'];

    return {
      data,
      value
    }
  },
}
</script>
```

## 示例：树型穿梭框

### 说明
通过穿梭框自定义接口可以实现树型穿梭框。




```vue

<template>
  <a-transfer :data="transferData" :default-value="value">
    <template #source="{data,selectedKeys,onSelect}">
      <a-tree
        :checkable="true"
        checked-strategy="child"
        :checked-keys="selectedKeys"
        :data="getTreeData(data)"
        @check="onSelect"
      />
    </template>
  </a-transfer>
</template>

<script>
export default {
  setup() {
    const treeData = [
      {
        title: 'Trunk 0-0',
        key: '0-0',
        children: [
          {
            title: 'Leaf 0-0-1',
            key: '0-0-1',
          },
          {
            title: 'Branch 0-0-2',
            key: '0-0-2',
            children: [
              {
                title: 'Leaf 0-0-2-1',
                key: '0-0-2-1'
              },
              {
                title: 'Leaf 0-0-2-2',
                key: '0-0-2-2',
              }
            ]
          },
        ],
      },
      {
        title: 'Trunk 0-1',
        key: '0-1',
        children: [
          {
            title: 'Branch 0-1-1',
            key: '0-1-1',
            children: [
              {
                title: 'Leaf 0-1-1-1',
                key: '0-1-1-1',
              },
              {
                title: 'Leaf 0-1-1-2',
                key: '0-1-1-2',
              },
            ]
          },
          {
            title: 'Leaf 0-1-2',
            key: '0-1-2',
          },
        ],
      },
    ];

    const getTransferData = (treeData = [], transferDataSource = []) => {
      treeData.forEach((item) => {
        if (item.children) getTransferData(item.children, transferDataSource);
        else transferDataSource.push({label: item.title, value: item.key});
      });
      return transferDataSource;
    };

    const getTreeData = (data = []) => {
      const values = data.map(item => item.value)

      const travel = (_treeData = []) => {
        const treeDataSource = []
        _treeData.forEach((item) => {
          if (item.children || values.includes(item.key)) {
            treeDataSource.push({title: item.title, key: item.key, children: travel(item.children)})
          }
        });
        return treeDataSource
      }

      return travel(treeData)
    }

    const transferData = getTransferData(treeData);


    const value = ['0-0-2-1'];

    return {
      transferData,
      value,
      getTreeData
    }
  },
}
</script>
```

## 示例：自定义标题栏

### 说明
通过 `source-title` ,`target-title` 插槽自定义标题栏的渲染内容




```vue
<template>
  <a-transfer :data="data" :default-value="value">
    <template
      #source-title="{
        countTotal,
        countSelected,
        checked,
        indeterminate,
        onSelectAllChange,
      }"
    >
      <div :style="styleHeader">
        Source Title {{ countSelected }}-{{ countTotal }}
        <a-checkbox
          :model-value="checked"
          :indeterminate="indeterminate"
          @change="onSelectAllChange"
        />
      </div>
    </template>

    <template #target-title="{ countTotal, countSelected, onClear }">
      <div :style="styleHeader">
        Target Title {{ countSelected }}-{{ countTotal }}
        <IconDelete @click="onClear" />
      </div>
    </template>
  </a-transfer>
</template>

<script>
import { IconDelete } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconDelete },
  setup() {
    const data = Array(8)
      .fill(undefined)
      .map((_, index) => ({
        value: `option${index + 1}`,
        label: `Option ${index + 1}`,
      }));
    const value = ['option1', 'option3', 'option5'];

    const styleHeader = {
      display: 'flex',
      alignItems: 'center',
      justifyContent: 'space-between',
      paddingRight: '8px'
    };

    return {
      styleHeader,
      data,
      value,
    };
  },
};
</script>
```

## API


### `<transfer>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|data|穿梭框的数据|`TransferItem[]`|`[]`||
|model-value **(v-model)**|目标选择框中的值|`string[]`|`-`||
|default-value|目标选择框中默认的值（非受控状态）|`string[]`|`[]`||
|selected **(v-model)**|选中的选项值|`string[]`|`-`||
|default-selected|默认选中的选项值（非受控状态）|`string[]`|`[]`||
|disabled|是否禁用|`boolean`|`false`||
|simple|是否开启简单模式（点击选项即移动）|`boolean`|`false`||
|one-way|是否开启单向模式（仅可移动到目标选择框）|`boolean`|`false`||
|show-search|是否显示搜索框|`boolean`|`false`||
|show-select-all|是否展示全选勾选框|`boolean`|`true`|2.39.0|
|title|源选择框和目标选择框的标题|`string[]`|`['Source', 'Target']`||
|source-input-search-props|源选择框的搜索框配置|`object`|`-`|2.51.1|
|target-input-search-props|目标选择框的搜索框配置|`object`|`-`|2.51.1|
### `<transfer>` 事件

|事件名|描述|参数|
|---|---|---|
|change|目标选择框的值改变时触发|value: `string[]`|
|select|选中的值改变时触发|selected: `string[]`|
|search|用户搜索时触发|value: `string`<br>type: `'target'\|'source'`|
### `<transfer>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|source|源面板|data: `TransferItem[]`<br>selectedKeys: `string[]`<br>onSelect: `(value: string[]) => void`|2.39.0|
|source-title|源标题插槽|countTotal: `number`<br>countSelected: `number`<br>searchValue: `string`<br>checked: `boolean`<br>indeterminate: `boolean`<br>onSelectAllChange: `(checked:boolean) => void`<br>onClear: `() => void`|2.45.0|
|to-target-icon|移至目标图标插槽|-|2.52.0|
|to-source-icon|移至源图标插槽|-|2.52.0|
|target|目标面板|data: `TransferItem[]`<br>selectedKeys: `string[]`<br>onSelect: `(value: string[]) => void`|2.39.0|
|target-title|目标标题插槽|countTotal: `number`<br>countSelected: `number`<br>searchValue: `string`<br>checked: `boolean`<br>indeterminate: `boolean`<br>onSelectAllChange: `(checked:boolean) => void`<br>onClear: `() => void`|2.45.0|
|item|选项|value: `string`<br>label: `string`||




### TransferItem

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|value|选项的值|`string`|`-`|
|label|选项的标签|`string`|`-`|
|disabled|是否禁用|`boolean`|`false`|
