---
name: arco-vue-layout
description: "Arco Design Vue 布局 Layout 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-layout>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 布局 Layout

来源组件：上游 `web-vue/components/layout`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-layout>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
典型的页面布局。




```vue
<template>
  <div class="layout-demo">
    <a-layout style="height: 400px;">
      <a-layout-header>Header</a-layout-header>
      <a-layout-content>Content</a-layout-content>
      <a-layout-footer>Footer</a-layout-footer>
    </a-layout>
    <br />
    <a-layout style="height: 400px;">
      <a-layout-header>Header</a-layout-header>
      <a-layout>
        <a-layout-sider theme="dark">Sider</a-layout-sider>
        <a-layout-content>Content</a-layout-content>
      </a-layout>
      <a-layout-footer>Footer</a-layout-footer>
    </a-layout>
    <br />
    <a-layout style="height: 400px;">
      <a-layout-header>Header</a-layout-header>
      <a-layout>
        <a-layout-content>Content</a-layout-content>
        <a-layout-sider>Sider</a-layout-sider>
      </a-layout>
      <a-layout-footer>Footer</a-layout-footer>
    </a-layout>
    <br />
    <a-layout style="height: 400px;">
      <a-layout-header>Header</a-layout-header>
      <a-layout>
        <a-layout-sider style="width: 64px;">Sider</a-layout-sider>
        <a-layout-sider style="width: 206px; margin-left: 1px;">Sider</a-layout-sider>
        <a-layout-content>Content</a-layout-content>
      </a-layout>
      <a-layout-footer>Footer</a-layout-footer>
    </a-layout>
  </div>
</template>
<style scoped>
.layout-demo :deep(.arco-layout-header),
.layout-demo :deep(.arco-layout-footer),
.layout-demo :deep(.arco-layout-sider-children),
.layout-demo :deep(.arco-layout-content) {
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: var(--color-white);
  font-size: 16px;
  font-stretch: condensed;
  text-align: center;
}


.layout-demo :deep(.arco-layout-header),
.layout-demo :deep(.arco-layout-footer) {
  height: 64px;
  background-color: var(--color-primary-light-4);
}

.layout-demo :deep(.arco-layout-sider) {
  width: 206px;
  background-color: var(--color-primary-light-3);
}

.layout-demo :deep(.arco-layout-content) {
  background-color: rgb(var(--arcoblue-6));
}
</style>
```

## 示例：自定义按钮 Icon

### 说明
通过设置 `Menu.Sider` 的 `trigger` 属性，实现自定义收起按钮的图标。




```vue
<template>
  <a-layout class="layout-demo">
    <a-layout-sider collapsible breakpoint="xl">
      <div class="logo" />
      <a-menu
        :default-open-keys="['1']"
        :default-selected-keys="['0_3']"
        :style="{ width: '100%' }"
        @menu-item-click="onClickMenuItem"
      >
        <a-menu-item key="0_1" disabled>
          <IconHome></IconHome>
          Menu 1
        </a-menu-item>
        <a-menu-item key="0_2">
          <IconCalendar></IconCalendar>
          Menu 2
        </a-menu-item>
        <a-menu-item key="0_3">
          <IconCalendar></IconCalendar>
          Menu 3
        </a-menu-item>
        <a-sub-menu key="1">
          <template #title>
            <IconCalendar></IconCalendar> Navigation 1
          </template>
          <a-menu-item key="1_1">Menu 1</a-menu-item>
          <a-menu-item key="1_2">Menu 2</a-menu-item>
          <a-sub-menu key="2" title="Navigation 2">
            <a-menu-item key="2_1">Menu 1</a-menu-item>
            <a-menu-item key="2_2">Menu 2</a-menu-item>
          </a-sub-menu>
          <a-sub-menu key="3" title="Navigation 3">
            <a-menu-item key="3_1">Menu 1</a-menu-item>
            <a-menu-item key="3_2">Menu 2</a-menu-item>
            <a-menu-item key="3_3">Menu 3</a-menu-item>
          </a-sub-menu>
        </a-sub-menu>
        <a-sub-menu key="4">
          <template #title>
            <IconCalendar></IconCalendar> Navigation 4
          </template>
          <a-menu-item key="4_1">Menu 1</a-menu-item>
          <a-menu-item key="4_2">Menu 2</a-menu-item>
          <a-menu-item key="4_3">Menu 3</a-menu-item>
        </a-sub-menu>
      </a-menu>
      <!-- trigger -->
      <template #trigger="{ collapsed }">
        <IconCaretRight v-if="collapsed"></IconCaretRight>
        <IconCaretLeft v-else></IconCaretLeft>
      </template>
    </a-layout-sider>
    <a-layout>
      <a-layout-header style="padding-left: 20px;">
        Header
      </a-layout-header >
      <a-layout style="padding: 0 24px;">
        <a-breadcrumb :style="{ margin: '16px 0' }">
          <a-breadcrumb-item>Home</a-breadcrumb-item>
          <a-breadcrumb-item>List</a-breadcrumb-item>
          <a-breadcrumb-item>App</a-breadcrumb-item>
        </a-breadcrumb>
        <a-layout-content>Content</a-layout-content>
        <a-layout-footer>Footer</a-layout-footer>
      </a-layout>
    </a-layout>
  </a-layout>
</template>
<script>
import { defineComponent } from 'vue';
import { Message} from '@arco-design/web-vue';
import {
  IconCaretRight,
  IconCaretLeft,
  IconHome,
  IconCalendar,
} from '@arco-design/web-vue/es/icon';

export default defineComponent({
  components: {
    IconCaretRight,
    IconCaretLeft,
    IconHome,
    IconCalendar,
  },
  methods: {
    onClickMenuItem(key) {
      Message.info({ content: `You select ${key}`, showIcon: true });
    }
  }
});
</script>
<style scoped>
.layout-demo {
  height: 500px;
  background: var(--color-fill-2);
  border: 1px solid var(--color-border);
}
.layout-demo :deep(.arco-layout-sider) .logo {
  height: 32px;
  margin: 12px 8px;
  background: rgba(255, 255, 255, 0.2);
}
.layout-demo :deep(.arco-layout-sider-light) .logo{
  background: var(--color-fill-2);
}
.layout-demo :deep(.arco-layout-header)  {
  height: 64px;
  line-height: 64px;
  background: var(--color-bg-3);
}
.layout-demo :deep(.arco-layout-footer) {
  height: 48px;
  color: var(--color-text-2);
  font-weight: 400;
  font-size: 14px;
  line-height: 48px;
}
.layout-demo :deep(.arco-layout-content) {
  color: var(--color-text-2);
  font-weight: 400;
  font-size: 14px;
  background: var(--color-bg-3);
}
.layout-demo :deep(.arco-layout-footer),
.layout-demo :deep(.arco-layout-content)  {
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: var(--color-white);
  font-size: 16px;
  font-stretch: condensed;
  text-align: center;
}
</style>
```

## 示例：自定义收起按钮

### 说明
设置`Menu.Sider` 的`hide-trigger`属性为`true`后，`Sider` 内置的缩起按钮不会显示。此时可自定义收起按钮。




```vue
<template>
  <a-layout class="layout-demo">
    <a-layout-sider
      hide-trigger
      collapsible
      :collapsed="collapsed"
    >
      <div class="logo" />
      <a-menu
        :defaultOpenKeys="['1']"
        :defaultSelectedKeys="['0_3']"
        :style="{ width: '100%' }"
        @menuItemClick="onClickMenuItem"
      >
        <a-menu-item key="0_1" disabled>
          <IconHome />
          Menu 1
        </a-menu-item>
        <a-menu-item key="0_2">
          <IconCalendar />
          Menu 2
        </a-menu-item>
        <a-menu-item key="0_3">
          <IconCalendar />
          Menu 3
        </a-menu-item>
        <a-sub-menu key="1">
          <template #title>
            <span><IconCalendar />Navigation 1</span>
          </template>
          <a-menu-item key="1_1">Menu 1</a-menu-item>
          <a-menu-item key="1_2">Menu 2</a-menu-item>
          <a-sub-menu key="2" title="Navigation 2">
            <a-menu-item key="2_1">Menu 1</a-menu-item>
            <a-menu-item key="2_2">Menu 2</a-menu-item>
          </a-sub-menu>
          <a-sub-menu key="3" title="Navigation 3">
            <a-menu-item key="3_1">Menu 1</a-menu-item>
            <a-menu-item key="3_2">Menu 2</a-menu-item>
            <a-menu-item key="3_3">Menu 3</a-menu-item>
          </a-sub-menu>
        </a-sub-menu>
        <a-sub-menu key="4">
          <template #title>
            <span><IconCalendar />Navigation 4</span>
          </template>
          <a-menu-item key="4_1">Menu 1</a-menu-item>
          <a-menu-item key="4_2">Menu 2</a-menu-item>
          <a-menu-item key="4_3">Menu 3</a-menu-item>
        </a-sub-menu>
      </a-menu>
    </a-layout-sider>
    <a-layout>
      <a-layout-header style="padding-left: 20px;">
        <a-button shape="round" @click="onCollapse">
          <IconCaretRight v-if="collapsed" />
          <IconCaretLeft v-else />
        </a-button>
      </a-layout-header>
      <a-layout style="padding: 0 24px;">
        <a-breadcrumb :style="{ margin: '16px 0' }">
          <a-breadcrumb-item>Home</a-breadcrumb-item>
          <a-breadcrumb-item>List</a-breadcrumb-item>
          <a-breadcrumb-item>App</a-breadcrumb-item>
        </a-breadcrumb>
        <a-layout-content>Content</a-layout-content>
        <a-layout-footer>Footer</a-layout-footer>
      </a-layout>
    </a-layout>
  </a-layout>
</template>
<script>
import { defineComponent, ref } from 'vue';
import { Message} from '@arco-design/web-vue';
import {
  IconCaretRight,
  IconCaretLeft,
  IconHome,
  IconCalendar,
} from '@arco-design/web-vue/es/icon';

export default defineComponent({
  components: {
    IconCaretRight,
    IconCaretLeft,
    IconHome,
    IconCalendar,
  },
  setup() {
    const collapsed = ref(false);
    const onCollapse = () => {
      collapsed.value = !collapsed.value;
    };
    return {
      collapsed,
      onCollapse,
      onClickMenuItem(key) {
        Message.info({ content: `You select ${key}`, showIcon: true });
      }
    };
  },
});
</script>
<style scoped>
.layout-demo {
  height: 500px;
  background: var(--color-fill-2);
  border: 1px solid var(--color-border);
}
.layout-demo :deep(.arco-layout-sider) .logo {
  height: 32px;
  margin: 12px 8px;
  background: rgba(255, 255, 255, 0.2);
}
.layout-demo :deep(.arco-layout-sider-light) .logo{
  background: var(--color-fill-2);
}
.layout-demo :deep(.arco-layout-header)  {
  height: 64px;
  line-height: 64px;
  background: var(--color-bg-3);
}
.layout-demo :deep(.arco-layout-footer) {
  height: 48px;
  color: var(--color-text-2);
  font-weight: 400;
  font-size: 14px;
  line-height: 48px;
}
.layout-demo :deep(.arco-layout-content) {
  color: var(--color-text-2);
  font-weight: 400;
  font-size: 14px;
  background: var(--color-bg-3);
}
.layout-demo :deep(.arco-layout-footer),
.layout-demo :deep(.arco-layout-content)  {
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: var(--color-white);
  font-size: 16px;
  font-stretch: condensed;
  text-align: center;
}
</style>
```

## 示例：响应式侧边栏

### 说明
左侧 Slider 可以结合 Menu 设置为展开/收起状态, 设置`breakpoint`可触发响应式收缩。




```vue
<template>
  <a-layout class="layout-demo">
    <a-layout-sider
      theme="dark"
      breakpoint="lg"
      :width="220"
      collapsible
      :collapsed="collapsed"
      @collapse="onCollapse"
    >
      <div class="logo" />
      <a-menu
        :defaultOpenKeys="['1']"
        :defaultSelectedKeys="['0_2']"
        @menuItemClick="onClickMenuItem"
      >
        <a-menu-item key="0_1" disabled>
          <IconHome />
          Menu 1
        </a-menu-item>
        <a-menu-item key="0_2">
          <IconCalendar />
          Menu 2
        </a-menu-item>
        <a-sub-menu key="1">
          <template #title>
            <span><IconCalendar />Navigation 1</span>
          </template>
          <a-menu-item key="1_1">Menu 1</a-menu-item>
          <a-menu-item key="1_2">Menu 2</a-menu-item>
          <a-sub-menu key="2" title="Navigation 2">
            <a-menu-item key="2_1">Menu 1</a-menu-item>
            <a-menu-item key="2_2">Menu 2</a-menu-item>
          </a-sub-menu>
          <a-sub-menu key="3" title="Navigation 3">
            <a-menu-item key="3_1">Menu 1</a-menu-item>
            <a-menu-item key="3_2">Menu 2</a-menu-item>
            <a-menu-item key="3_3">Menu 3</a-menu-item>
          </a-sub-menu>
        </a-sub-menu>
        <a-sub-menu key="4">
          <template #title>
            <span><IconCalendar />Navigation 4</span>
          </template>
          <a-menu-item key="4_1">Menu 1</a-menu-item>
          <a-menu-item key="4_2">Menu 2</a-menu-item>
          <a-menu-item key="4_3">Menu 3</a-menu-item>
        </a-sub-menu>
      </a-menu>
    </a-layout-sider>
    <a-layout>
      <a-layout-header>
        <a-menu
          :openKeys="['1']"
          :selectedKeys="['0_2']"
          mode='horizontal'
        >
          <a-menu-item key="0_1" disabled>
            <IconHome />
            Menu 1
          </a-menu-item>
          <a-menu-item key="0_2">
            <IconCalendar />
            Menu 2
          </a-menu-item>
          <a-sub-menu key="1">
            <template #title>
              <span><IconCalendar />Navigation 1</span>
            </template>
            <a-menu-item key="1_1">Menu 1</a-menu-item>
            <a-menu-item key="1_2">Menu 2</a-menu-item>
            <a-sub-menu key="2" title="Navigation 2">
              <a-menu-item key="2_1">Menu 1</a-menu-item>
              <a-menu-item key="2_2">Menu 2</a-menu-item>
            </a-sub-menu>
            <a-sub-menu key="3" title="Navigation 3">
              <a-menu-item key="3_1">Menu 1</a-menu-item>
              <a-menu-item key="3_2">Menu 2</a-menu-item>
              <a-menu-item key="3_3">Menu 3</a-menu-item>
            </a-sub-menu>
          </a-sub-menu>
          <a-sub-menu key="4">
            <template #title>
              <span><IconCalendar />Navigation 4</span>
            </template>
            <a-menu-item key="4_1">Menu 1</a-menu-item>
            <a-menu-item key="4_2">Menu 2</a-menu-item>
            <a-menu-item key="4_3">Menu 3</a-menu-item>
          </a-sub-menu>
        </a-menu>
      </a-layout-header>
      <a-layout style="padding: 0 24px">
        <a-breadcrumb :style="{ margin: '16px 0' }">
          <a-breadcrumb-item>Home</a-breadcrumb-item>
          <a-breadcrumb-item>List</a-breadcrumb-item>
          <a-breadcrumb-item>App</a-breadcrumb-item>
        </a-breadcrumb>
        <a-layout-content>Content</a-layout-content>
        <a-layout-footer>Footer</a-layout-footer>
      </a-layout>
    </a-layout>
  </a-layout>
</template>
<script>
import { defineComponent, ref } from 'vue';
import { Message } from '@arco-design/web-vue';
import {
  IconHome,
  IconCalendar,
} from '@arco-design/web-vue/es/icon';

export default defineComponent({
  components: {
    IconHome,
    IconCalendar,
  },
  setup() {
    const collapsed = ref(false);
    const onCollapse = (val, type) => {
      const content = type === 'responsive' ? '触发响应式收缩' : '点击触发收缩';
      Message.info({
        content,
        duration: 2000,
      });
      collapsed.value = val;
    }
    return {
      collapsed,
      onCollapse,
      onClickMenuItem(key) {
        Message.info({ content: `You select ${key}`, showIcon: true });
      }
    };
  }
});
</script>
<style scoped>
.layout-demo {
  height: 500px;
  background: var(--color-fill-2);
  border: 1px solid var(--color-border);
}
.layout-demo :deep(.arco-layout-sider) .logo {
  height: 32px;
  margin: 12px 8px;
  background: rgba(255, 255, 255, 0.2);
}
.layout-demo :deep(.arco-layout-sider-light) .logo{
  background: var(--color-fill-2);
}
.layout-demo :deep(.arco-layout-header)  {
  height: 64px;
  line-height: 64px;
  background: var(--color-bg-3);
}
.layout-demo :deep(.arco-layout-footer) {
  height: 48px;
  color: var(--color-text-2);
  font-weight: 400;
  font-size: 14px;
  line-height: 48px;
}
.layout-demo :deep(.arco-layout-content) {
  color: var(--color-text-2);
  font-weight: 400;
  font-size: 14px;
  background: var(--color-bg-3);
}
.layout-demo :deep(.arco-layout-footer),
.layout-demo :deep(.arco-layout-content)  {
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: var(--color-white);
  font-size: 16px;
  font-stretch: condensed;
  text-align: center;
}
</style>
```

## 示例：可伸缩侧边栏

### 说明
可以用鼠标进行拖拽放大缩小的侧边栏，需要用到的参数：`resizeDirections`。




```vue
<template>
  <div class="layout-demo">
    <a-layout>
      <a-layout-header>Header</a-layout-header>
      <a-layout>
        <a-layout-sider :resize-directions="['right']">
          Sider
        </a-layout-sider>
        <a-layout-content>Content</a-layout-content>
      </a-layout>
      <a-layout-footer>Footer</a-layout-footer>
    </a-layout>
  </div>
</template>
<style scoped>
.layout-demo :deep(.arco-layout-header),
.layout-demo :deep(.arco-layout-footer),
.layout-demo :deep(.arco-layout-sider-children),
.layout-demo :deep(.arco-layout-content) {
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: var(--color-white);
  font-size: 16px;
  font-stretch: condensed;
  text-align: center;
}


.layout-demo :deep(.arco-layout-header),
.layout-demo :deep(.arco-layout-footer) {
  height: 64px;
  background-color: var(--color-primary-light-4);
}

.layout-demo :deep(.arco-layout-sider) {
  width: 206px;
  background-color: var(--color-primary-light-3);
  min-width: 150px;
  max-width: 500px;
  height: 200px;
}

.layout-demo :deep(.arco-layout-content) {
  background-color: rgb(var(--arcoblue-6));
}
</style>
```

## API


### `<layout>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|has-sider|表示子元素里有 Sider，一般不用指定。可用于服务端渲染时避免样式闪动|`boolean`|`false`|




### `<layout-header>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|default|内容|-|




### `<layout-content>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|default|内容|-|




### `<layout-footer>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|default|内容|-|




### `<layout-sider>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|theme|主题颜色|`'dark' \| 'light'`|`'light'`|
|collapsed|当前收起状态|`boolean`|`-`|
|default-collapsed|默认的收起状态|`boolean`|`false`|
|collapsible|是否可收起|`boolean`|`false`|
|width|宽度|`number`|`200`|
|collapsed-width|收缩宽度|`number`|`48`|
|reverse-arrow|翻转折叠提示箭头的方向，当 Sider 在右边时可以使用|`boolean`|`false`|
|breakpoint|触发响应式布局的断点, 详见[响应式栅格](/vue/component/grid)|`'xxl' \| 'xl' \| 'lg' \| 'md' \| 'sm' \| 'xs'`|`-`|
|resize-directions|可以用 ResizeBox 替换原生的 `aside` 标签，这个参数即 ResizeBox的 `directions` 参数。详情请看 [ResizeBox](/vue/component/resize-box)。|`Array<'left' \| 'right' \| 'top' \| 'bottom'>`|`-`|
|hide-trigger|隐藏底部折叠触发器|`boolean`|`false`|
### `<layout-sider>` 事件

|事件名|描述|参数|
|---|---|---|
|collapse|展开-收起时的事件，有点击 trigger 以及响应式反馈两种方式可以触发|collapsed: `boolean`<br>type: `'clickTrigger'\|'responsive'`|
|breakpoint|触发响应式布局断点时的事件|collapsed: `boolean`|
### `<layout-sider>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|trigger|自定义底部折叠触发器|collapsed: `boolean`|
