---
name: arco-vue-descriptions
description: "Arco Design Vue 描述列表 Descriptions 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-descriptions>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 描述列表 Descriptions

来源组件：上游 `web-vue/components/descriptions`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-descriptions>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
简单地成组展示多个只读字段，一般用于详情页的信息。




```vue
<template>
  <a-space direction="vertical" size="large" fill>
    <a-descriptions :data="data" title="User Info" layout="inline-horizontal" />
    <a-descriptions title="User Info" :column="{xs:1, md:3, lg:4}">
      <a-descriptions-item v-for="item of data" :label="item.label" :span="item.span ?? 1">
        <a-tag>{{ item.value }}</a-tag>
      </a-descriptions-item>
    </a-descriptions>
  </a-space>
</template>

<script>
export default {
  setup() {
    const data = [{
      label: 'Name',
      value: 'Socrates',
      span: 3,
    }, {
      label: 'Mobile',
      value: '123-1234-1234',
    }, {
      label: 'Residence',
      value: 'Beijing'
    }, {
      label: 'Hometown',
      value: 'Beijing',
    }, {
      label: 'Address',
      value: 'Yingdu Building, Zhichun Road, Beijing'
    }];

    return {
      data
    }
  },
}
</script>
```

## 示例：单列样式

### 说明
单列的描述列表样式。




```vue
<template>
  <a-radio-group type="button" v-model="size">
    <a-radio value="mini">mini</a-radio>
    <a-radio value="small">small</a-radio>
    <a-radio value="medium">medium</a-radio>
    <a-radio value="large">large</a-radio>
  </a-radio-group>
  <a-descriptions style="margin-top: 20px" :data="data" :size="size" title="User Info" :column="1"/>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const size = ref('medium');

    const data = [{
      label: 'Name',
      value: 'Socrates',
    }, {
      label: 'Mobile',
      value: '123-1234-1234',
    }, {
      label: 'Residence',
      value: 'Beijing'
    }, {
      label: 'Hometown',
      value: 'Beijing',
    }, {
      label: 'Address',
      value: 'Yingdu Building, Zhichun Road, Beijing'
    }];

    return {
      data,
      size
    }
  },
}
</script>
```

## 示例：标签文本对齐

### 说明
标签文本可以设置左对齐右对齐，也可以设置垂直的排列方式。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-descriptions :data="data" title="User Info" align="right" />
    <a-descriptions :data="data" title="User Info" :align="{ label: 'right' }" />
    <a-descriptions :data="data" title="User Info" layout="inline-vertical" />
  </a-space>
</template>

<script>
export default {
  setup() {
    const data = [{
      label: 'Name',
      value: 'Socrates',
    }, {
      label: 'Mobile',
      value: '123-1234-1234',
    }, {
      label: 'Residence',
      value: 'Beijing'
    }, {
      label: 'Hometown',
      value: 'Beijing',
    }, {
      label: 'Address',
      value: 'Yingdu Building, Zhichun Road, Beijing'
    }];

    return {
      data
    }
  },
}
</script>
```

## 示例：带边框样式

### 说明
带边框和背景颜色的列表。




```vue
<template>
  <a-descriptions :data="data" title="User Info" bordered/>
</template>

<script>
export default {
  setup() {
    const data = [{
      label: 'Name',
      value: 'Socrates',
    }, {
      label: 'Mobile',
      value: '123-1234-1234',
    }, {
      label: 'Residence',
      value: 'Beijing'
    }, {
      label: 'Hometown',
      value: 'Beijing',
    }, {
      label: 'Address',
      value: 'Yingdu Building, Zhichun Road, Beijing'
    }];

    return {
      data
    }
  },
}
</script>
```

## 示例：布局模式

### 说明
有水平排列、垂直排列、行内水平排列、行内垂直排列四种布局模式。




```vue

<template>
  <a-radio-group type="button" v-model="size">
    <a-radio value="mini">mini</a-radio>
    <a-radio value="small">small</a-radio>
    <a-radio value="medium">medium</a-radio>
    <a-radio value="large">large</a-radio>
  </a-radio-group>
  <div style="margin-top: 20px">
    <a-descriptions :data="data" :size="size" title="User Info (horizontal)" bordered />
    <a-descriptions :data="data" :size="size" title="User Info (inline-horizontal)" layout="inline-horizontal" bordered />
    <a-descriptions :data="data" :size="size" title="User Info (vertical)" layout="vertical" bordered />
    <a-descriptions :data="data" :size="size" title="User Info (inline-vertical)" layout="inline-vertical" bordered />
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const size = ref('medium');

    const data = [{
      label: 'Name',
      value: 'Socrates',
    }, {
      label: 'Mobile',
      value: '123-1234-1234',
    }, {
      label: 'Residence',
      value: 'Beijing'
    }, {
      label: 'Hometown',
      value: 'Beijing',
    }, {
      label: 'Address',
      value: 'Yingdu Building, Zhichun Road, Beijing'
    }];

    return {
      data,
      size
    }
  },
}
</script>
```

## 示例：布局示例

### 说明
`span` 所占列数大于 `column` 可放置的数据个数时，`span` 会被设置为 `column` 的值，当行剩余列数不够放置下一列时将自动换行，每行末尾列会自动填充剩余量。




```vue
<template>
  <a-form :model="form" auto-label-width>
    <a-form-item label="size">
      <a-radio-group v-model="form.size" type="button" :options="sizeOptions" />
    </a-form-item>

    <a-form-item label="layout">
      <a-radio-group
        v-model="form.layout"
        type="button"
        :options="layoutOptions"
      />
    </a-form-item>

    <a-form-item label="table-layout">
      <a-radio-group
        v-model="form.tableLayout"
        type="button"
        :options="['auto', 'fixed']"
      />
    </a-form-item>

    <a-form-item label="column">
      <a-radio-group
        v-model="form.column"
        type="button"
        :options="columnOptions"
      />
    </a-form-item>

    <a-form-item label="firstSpan">
      <a-radio-group
        v-model="form.firstSpan"
        type="button"
        :options="firstSpanOptions"
      />
    </a-form-item>
  </a-form>
  <div style="margin-top: 20px">
    <a-descriptions
      title="Layout Example"
      :size="form.size"
      :column="form.column"
      :layout="form.layout"
      :table-layout="form.tableLayout"
      bordered
    >
      <a-descriptions-item label="Item1" :span="form.firstSpan">
        <div>Span：{{form.firstSpan}}
          <span v-if="form.firstSpan > form.column" style="color: red;">
            Exceeds Column, set to Column size
          </span>
        </div>
      </a-descriptions-item>
      <a-descriptions-item label="Item2" :span="2">Span：2</a-descriptions-item>
      <a-descriptions-item label="Item3" :span="3">Span：3</a-descriptions-item>
      <a-descriptions-item label="Item4" :span="2">Span：2</a-descriptions-item>
      <a-descriptions-item label="Item5" :span="1">Span：1</a-descriptions-item>
      <a-descriptions-item label="Item6" :span="1">Span：1</a-descriptions-item>
    </a-descriptions>
  </div>
</template>

<script setup>
import { reactive } from 'vue';

const form = reactive({
  size: 'medium',
  layout: 'horizontal',
  column: 4,
  tableLayout: 'auto',
  firstSpan: 2
});

const layoutOptions = [
  'horizontal',
  'inline-horizontal',
  'vertical',
  'inline-vertical',
];
const columnOptions = [1, 2, 3, 4, 5];
const firstSpanOptions = [1, 2, 3, 4, 5];
const sizeOptions = ['mini', 'small', 'medium', 'large'];
</script>
```

## API


### `<descriptions>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|data|描述列表的数据|`DescData[]`|`[]`||
|column|每行放置的数据个数。2.20.0 版本支持响应式配置，配置可参考 Grid|`number \| ResponsiveValue`|`3`||
|title|描述列表的标题|`string`|`-`||
|layout|描述列表的排列方式|`'horizontal' \| 'vertical' \| 'inline-horizontal' \| 'inline-vertical'`|`'horizontal'`||
|align|文字的对齐位置|`TextAlign \| { label?: TextAlign; value?: TextAlign }`|`'left'`||
|size|描述列表的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`-`||
|bordered|是否显示边框|`boolean`|`false`||
|label-style|数据标签的样式|`CSSProperties`|`-`||
|value-style|数据内容的样式|`CSSProperties`|`-`||
|table-layout|描述中表格样式的 `layout-fixed`，当设置成 `fixed` 时，宽度会均分。|`'auto' \| 'fixed'`|`'auto'`|2.38.0|
### `<descriptions>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|value|数据内容|value: `string`<br>index: `number`<br>data: `DescData`|
|label|数据标签|label: `string`<br>index: `number`<br>data: `DescData`|
|title|标题|-|




### `<descriptions-item>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|span|所占列数|`number`|`1`|2.18.0|
|label|标签|`string`|`-`|2.18.0|
### `<descriptions-item>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|label|标签|-|2.18.0|




### DescData

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|label|标签|`string \| RenderFunction`|`-`|
|value|数据|`string \| RenderFunction`|`-`|
|span|所占列数|`number`|`1`|
