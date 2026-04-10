---
name: arco-vue-tabs
description: "Arco Design Vue 标签页 Tabs 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-tabs>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 标签页 Tabs

来源组件：上游 `web-vue/components/tabs`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-tabs>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
标签页的基本使用方法。




```vue
<template>
  <a-tabs default-active-key="2">
    <a-tab-pane key="1" title="Tab 1">
      Content of Tab Panel 1
    </a-tab-pane>
    <a-tab-pane key="2" title="Tab 2">
      Content of Tab Panel 2
    </a-tab-pane>
    <a-tab-pane key="3">
      <template #title>Tab 3</template>
      Content of Tab Panel 3
    </a-tab-pane>
  </a-tabs>
</template>
```

## 示例：带图标的页签

### 说明
带有图标的标签页。




```vue
<template>
  <a-tabs>
    <a-tab-pane key="1">
      <template #title>
        <icon-calendar/> Tab 1
      </template>
      Content of Tab Panel 1
    </a-tab-pane>
    <a-tab-pane key="2">
      <template #title>
        <icon-clock-circle/> Tab 2
      </template>
      Content of Tab Panel 2
    </a-tab-pane>
    <a-tab-pane key="3">
      <template #title>
        <icon-user/> Tab 3
      </template>
      Content of Tab Panel 3
    </a-tab-pane>
  </a-tabs>
</template>
```

## 示例：位置

### 说明
通过 `position` 属性可以自定义标签栏的位置。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-radio-group v-model="position" type="button">
      <a-radio value="top">Top</a-radio>
      <a-radio value="right">Right</a-radio>
      <a-radio value="bottom">Bottom</a-radio>
      <a-radio value="left">Left</a-radio>
    </a-radio-group>
    <a-tabs :position="position">
      <a-tab-pane key="1" title="Tab 1">
        Content of Tab Panel 1
      </a-tab-pane>
      <a-tab-pane key="2" title="Tab 2">
        Content of Tab Panel 2
      </a-tab-pane>
      <a-tab-pane key="3" title="Tab 3">
        Content of Tab Panel 3
      </a-tab-pane>
    </a-tabs>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const position = ref('top');

    return {
      position
    }
  },
}
</script>
```

## 示例：不同类型

### 说明
通过 `type` 可以设置标签的类型。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-radio-group v-model="type" type="button">
      <a-radio value="line">Line</a-radio>
      <a-radio value="card">Card</a-radio>
      <a-radio value="card-gutter">Card Gutter</a-radio>
      <a-radio value="text">Text</a-radio>
      <a-radio value="rounded">Rounded</a-radio>
      <a-radio value="capsule">Capsule</a-radio>
    </a-radio-group>
    <a-radio-group v-model="size" type="button">
      <a-radio value="mini">Mini</a-radio>
      <a-radio value="small">Small</a-radio>
      <a-radio value="medium">Medium</a-radio>
      <a-radio value="large">Large</a-radio>
    </a-radio-group>
    <a-tabs :type="type" :size="size">
      <a-tab-pane key="1" title="Tab 1">
        Content of Tab Panel 1
      </a-tab-pane>
      <a-tab-pane key="2" title="Tab 2">
        Content of Tab Panel 2
      </a-tab-pane>
      <a-tab-pane key="3" title="Tab 3">
        Content of Tab Panel 3
      </a-tab-pane>
    </a-tabs>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const type = ref('line');
    const size = ref('medium');

    return {
      type,
      size
    }
  },
}
</script>
```

## 示例：懒加载

### 说明
通过设置 lazy-load 属性，可以让面板在首次激活时渲染。




```vue
<template>
  <a-tabs default-active-key="2" lazy-load>
    <a-tab-pane key="1" title="Tab 1">
      Content of Tab Panel 1
    </a-tab-pane>
    <a-tab-pane key="2" title="Tab 2">
      Content of Tab Panel 2
    </a-tab-pane>
    <a-tab-pane key="3" title="Tab 3">
      Content of Tab Panel 3
    </a-tab-pane>
  </a-tabs>
</template>
```

## 示例：附加内容

### 说明
通过 `extra` 插槽可以自定义额外显示内容。




```vue
<template>
  <a-tabs>
    <template #extra>
      <a-button>Action</a-button>
    </template>
    <a-tab-pane key="1" title="Tab 1">
      Content of Tab Panel 1
    </a-tab-pane>
    <a-tab-pane key="2" title="Tab 2">
      Content of Tab Panel 2
    </a-tab-pane>
    <a-tab-pane key="3" title="Tab 3">
      Content of Tab Panel 3
    </a-tab-pane>
  </a-tabs>
</template>
```

## 示例：动态增减标签页

### 说明
通过设置 `:editable="true"` 可以开启动态增减标签页。仅在 `line` | `card` | `card-gutter` 生效




```vue

<template>
  <a-tabs type="card-gutter" :editable="true" @add="handleAdd" @delete="handleDelete" show-add-button auto-switch>
    <a-tab-pane v-for="(item, index) of data" :key="item.key" :title="item.title" :closable="index!==2">
      {{ item?.content }}
    </a-tab-pane>
  </a-tabs>
</template>

<script>
import { ref } from 'vue';

let count = 5;

export default {
  setup() {
    const data = ref([
      {
        key: '1',
        title: 'Tab 1',
        content: 'Content of Tab Panel 1'
      },
      {
        key: '2',
        title: 'Tab 2',
        content: 'Content of Tab Panel 2'
      },
      {
        key: '3',
        title: 'Tab 3',
        content: 'Content of Tab Panel 3'
      },
      {
        key: '4',
        title: 'Tab 4',
        content: 'Content of Tab Panel 4'
      }
    ]);

    const handleAdd = () => {
      const number = count++;
      data.value = data.value.concat({
        key: `${number}`,
        title: `New Tab ${number}`,
        content: `Content of New Tab Panel ${number}`
      })
    };
    const handleDelete = (key) => {
      data.value = data.value.filter(item => item.key !== key)
    };

    return {
      data,
      handleAdd,
      handleDelete
    }
  },
}
</script>
```

## 示例：触发方式

### 说明
通过 `trigger` 指定触发方式。




```vue
<template>
  <a-radio-group v-model="trigger">
    <a-radio value="click">click</a-radio>
    <a-radio value="hover">hover</a-radio>
  </a-radio-group>
  <a-tabs default-active-key="1" :trigger="trigger">
    <a-tab-pane key="1" title="Tab 1"> Content of Tab Panel 1 </a-tab-pane>
    <a-tab-pane key="2" title="Tab 2"> Content of Tab Panel 2 </a-tab-pane>
    <a-tab-pane key="3">
      <template #title>Tab 3</template>
      Content of Tab Panel 3
    </a-tab-pane>
  </a-tabs>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const trigger = ref('click');
    return {
      trigger,
    };
  },
};
</script>
```

## 示例：滚动

### 说明
支持通过滚轮或者触摸板进行滚动操作，且可以通过 `scrollPosition` 属性设置滚动位置。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-radio-group v-model="position" type="button">
      <a-radio value="left">Left</a-radio>
      <a-radio value="top">Top</a-radio>
      <a-radio value="right">Right</a-radio>
      <a-radio value="bottom">Bottom</a-radio>
    </a-radio-group>
    <a-radio-group v-model="scrollPosition" type="button">
      <a-radio value="auto">auto</a-radio>
      <a-radio value="start">start</a-radio>
      <a-radio value="center">center</a-radio>
      <a-radio value="end">end</a-radio>
    </a-radio-group>
    <a-button @click="changeActive"> Change: {{activeKey}}</a-button>
  </a-space>
  <a-tabs
    v-model:activeKey="activeKey"
    :position="position"
    :scrollPosition="scrollPosition"
    style="width: 100%;height: 300px;margin-top: 20px"
  >
    <a-tab-pane v-for="tab in tabs" :key="tab.key" :title="tab.title">
      {{ tab.content }}
    </a-tab-pane>
  </a-tabs>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const position = ref('top');
    const scrollPosition = ref('auto');
    const activeKey = ref('Tab1');
    const tabs = Array.from({ length: 30 }, (v, i) => {
      return {
        key: `Tab${i + 1}`,
        title: `Tab ${i + 1}`,
        content: `Content of Tab Panel ${i + 1}`
      }
    });

    const changeActive = () => {
      activeKey.value = `Tab${Math.floor(Math.random() * 30) + 1}`;
    }

    return {
      tabs,
      position,
      scrollPosition,
      activeKey,
      changeActive
    }
  },
}
</script>
```

## API


### `<tabs>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|active-key **(v-model)**|当前选中的标签的 `key`|`string\|number`|`-`||
|default-active-key|默认选中的标签的`key`（非受控状态，为空时选中第一个标签页）|`string\|number`|`-`||
|position|选项卡的位置|`'left' \| 'right' \| 'top' \| 'bottom'`|`'top'`||
|size|选项卡的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`-`||
|type|选项卡的类型|`'line' \| 'card' \| 'card-gutter' \| 'text' \| 'rounded' \| 'capsule'`|`'line'`||
|direction|选项卡的方向|`'horizontal' \| 'vertical'`|`'horizontal'`||
|editable|是否开启可编辑模式|`boolean`|`false`||
|show-add-button|是否显示增加按钮（仅在可编辑模式可用）|`boolean`|`false`||
|destroy-on-hide|是否在不显示标签时销毁内容|`boolean`|`false`|2.27.0|
|lazy-load|是否在首次展示标签时挂载内容|`boolean`|`false`||
|justify|高度撑满容器，只在水平模式下生效。|`boolean`|`false`||
|animation|是否开启选项内容过渡动画|`boolean`|`false`||
|header-padding|选项卡头部是否存在水平边距。仅对 `type` 等于 `line`、`text` 类型的选项卡生效|`boolean`|`true`|2.10.0|
|auto-switch|创建标签后是否切换到新标签（最后一个）|`boolean`|`false`|2.18.0|
|hide-content|是否隐藏内容|`boolean`|`false`|2.25.0|
|trigger|触发方式|`'hover' \| 'click'`|`'click'`|2.34.0|
|scroll-position|被选中 tab 的滚动位置，默认 auto 即会将 activeTab 滚动到可见区域，但不会特意做位置调整|`'start' \| 'end' \| 'center' \| 'auto' \| number`|`'auto'`||
### `<tabs>` 事件

|事件名|描述|参数|
|---|---|---|
|change|当前标签值改变时触发|key: ` string \| number `|
|tab-click|用户点击标签时触发|key: ` string \| number `|
|add|用户点击增加按钮时触发|-|
|delete|用户点击删除按钮时触发|key: ` string \| number `|
### `<tabs>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|extra|选项卡额外内容|-|




### `<tab-pane>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|title|选项卡的标题|`string`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|closable|是否允许关闭此选项卡（仅在可编辑模式生效）|`boolean`|`true`||
|destroy-on-hide|是否在不显示标签时销毁内容|`boolean`|`false`|2.27.0|
### `<tab-pane>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|title|选项卡标题|-|
