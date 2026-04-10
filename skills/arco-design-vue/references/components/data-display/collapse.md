---
name: arco-vue-collapse
description: "Arco Design Vue 折叠面板 Collapse 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-collapse>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 折叠面板 Collapse

来源组件：上游 `web-vue/components/collapse`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-collapse>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
用于将复杂的内容区域分组和隐藏，可折叠或展开。默认可以展开多个面板。




```vue
<template>
  <a-collapse :default-active-key="['1', 2]">
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." :key="2" disabled>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="3">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
  </a-collapse>
</template>
```

## 示例：手风琴模式

### 说明
通过 `accordion` 开启手风琴模式，同时只能打开一个面板。




```vue
<template>
  <a-collapse :default-active-key="[1]" accordion>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="2">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="3">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
  </a-collapse>
</template>
```

## 示例：嵌套面板

### 说明
面板多层嵌套。




```vue
<template>
  <a-collapse :default-active-key="['1', 2]" destroy-on-hide>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
      <a-collapse :default-active-key="['1.1']" destroy-on-hide>
        <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1.1">
          <div>Beijing Toutiao Technology Co., Ltd.</div>
        </a-collapse-item>
        <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1.2">
          <div>Beijing Toutiao Technology Co., Ltd.</div>
        </a-collapse-item>
      </a-collapse>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." :key="2">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="3">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
  </a-collapse>
</template>
```

## 示例：无边框模式

### 说明
通过设置 `bordered="false"` 隐藏边框。




```vue
<template>
  <a-collapse :default-active-key="['1']" :bordered="false">
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="2" disabled>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="3">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
  </a-collapse>
</template>
```

## 示例：额外节点

### 说明
通过 `extra` 可以设置额外节点。`extra` 单击可以以设置 `stop` 修饰符，以阻止当前项目展开。




```vue
<template>
  <a-collapse>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
      <template #extra>
        <icon-copy />
      </template>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." :key="2">
      <template #extra>
        <a-button type="primary" size="mini" @click.stop="sayHello">hello</a-button>
      </template>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="3">
      <template #extra>
        <a-tag size="small">city</a-tag>
      </template>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
  </a-collapse>
</template>

<script>
import { Message } from '@arco-design/web-vue';

export default {
  setup() {
    const sayHello = () => {
      Message.info('hello');
    };

    return {
      sayHello,
    };
  },
};
</script>
```

## 示例：展开图标

### 说明
为展开项自定义展开图标




```vue
<template>
  <a-collapse :default-active-key="['1', 2]">
    <template #expand-icon="{ active }">
      <icon-face-smile-fill v-if="active"/>
      <icon-face-frown-fill v-else/>
    </template>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
      <template #expand-icon="{ active }">
        <icon-double-down v-if="active"/>
        <icon-double-right v-else/>
      </template>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." :key="2">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="3">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
  </a-collapse>
</template>
```

## 示例：自定义样式

### 说明
自定义面板样式。




```vue
<template>
  <a-collapse :default-active-key="['1', 2]" :bordered="false">
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." :style="customStyle" key="1">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." :style="customStyle" :key="2">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." :style="customStyle" key="3">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
  </a-collapse>
</template>

<script>
export default {
  setup() {
    const customStyle = {
      borderRadius: '6px',
      marginBottom: '18px',
      border: 'none',
      overflow: 'hidden',
    }

    return {
      customStyle
    }
  }
}
</script>
```

## 示例：展开图标位置

### 说明
通过 `expand-icon-position` 属性设置展开图标的位置。




```vue
<template>
  <a-space direction="vertical" :style="{ width: '100%' }">
    <a-space>
      <a-radio-group type="button" v-model="position">
        <a-radio value="left">Left</a-radio>
        <a-radio value="right">Right</a-radio>
      </a-radio-group>
      <a-checkbox v-model="hideIcon">Hide Expand Icon</a-checkbox>
    </a-space>
    <a-collapse
      :default-active-key="['1']"
      :expand-icon-position="position"
      :show-expand-icon="!hideIcon"
    >
      <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
        <template #expand-icon>
          <icon-plus />
        </template>
        <template #extra>
          <a-tag size="small">city</a-tag>
        </template>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
      </a-collapse-item>
      <a-collapse-item
        header="Beijing Toutiao Technology Co., Ltd."
        key="2"
        disabled
      >
        <div>Beijing Toutiao Technology Co., Ltd.</div>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
      </a-collapse-item>
      <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="3">
        <div>Beijing Toutiao Technology Co., Ltd.</div>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
      </a-collapse-item>
    </a-collapse>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const position = ref('left');
    const hideIcon = ref(false);

    return {
      position,
      hideIcon,
    };
  },
};
</script>
```

## 示例：隐藏时销毁

### 说明
通过设置 `destroy-on-hide` 可以让面板内容在隐藏时销毁。




```vue
<template>
  <a-collapse :default-active-key="['1', 2]" destroy-on-hide>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." :key="2">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
    <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="3" :show-expand-icon="false">
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
      <div>Beijing Toutiao Technology Co., Ltd.</div>
    </a-collapse-item>
  </a-collapse>
</template>
```

## API


### `<collapse>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|active-key **(v-model)**|当前展开的面板的 `key`|`(string \| number)[]`|`-`||
|default-active-key|默认展开的面板的 `key` （非受控模式）|`(string \| number)[]`|`[]`||
|accordion|是否开启手风琴模式|`boolean`|`false`||
|show-expand-icon|是否显示展开图标|`boolean`|`-`|2.33.0|
|expand-icon-position|展开图标显示的位置|`'left' \| 'right'`|`'left'`||
|bordered|是否显示边框|`boolean`|`true`||
|destroy-on-hide|是否在隐藏时销毁内容|`boolean`|`false`|2.27.0|
### `<collapse>` 事件

|事件名|描述|参数|
|---|---|---|
|change|展开的面板发生改变时触发|activeKey: `(string \| number)[]`<br>ev: `Event`|




### `<collapse-item>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|header|面板的标题|`string`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|show-expand-icon|是否显示展开图标|`boolean`|`true`||
|destroy-on-hide|是否在隐藏时销毁内容|`boolean`|`false`|2.27.0|
### `<collapse-item>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|extra|额外内容|-||
|expand-icon|展开图标|active: `boolean`<br>disabled: `boolean`<br>position: `'left' \| 'right'`|2.33.0|
|header|面板的标题|-||



## FAQ

### `<CollapseItem>` 组件的 `key` 属性为必填
在 `<Collapse>` 组件中每个 `<CollapseItem>` 都需要指定唯一的 `key` 属性，`key` 对应 `activeKey` 中的值。
