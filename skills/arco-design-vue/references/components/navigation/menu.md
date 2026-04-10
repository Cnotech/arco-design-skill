---
name: arco-vue-menu
description: "Arco Design Vue 菜单 Menu 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-menu>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 菜单 Menu

来源组件：上游 `web-vue/components/menu`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-menu>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：顶部导航菜单

### 说明
设置 `mode` 为 `horizontal` 时，使用水平菜单。




```vue
<template>
  <div class="menu-demo">
    <a-menu mode="horizontal" :default-selected-keys="['1']">
      <a-menu-item key="0" :style="{ padding: 0, marginRight: '38px' }" disabled>
        <div
          :style="{
            width: '80px',
            height: '30px',
            borderRadius: '2px',
            background: 'var(--color-fill-3)',
            cursor: 'text',
          }"
        />
      </a-menu-item>
      <a-menu-item key="1">Home</a-menu-item>
      <a-menu-item key="2">Solution</a-menu-item>
      <a-menu-item key="3">Cloud Service</a-menu-item>
      <a-menu-item key="4">Cooperation</a-menu-item>
    </a-menu>
  </div>
</template>
<style scoped>
.menu-demo {
  box-sizing: border-box;
  width: 100%;
  padding: 40px;
  background-color: var(--color-neutral-2);
}
</style>
```

## 示例：深色模式导航

### 说明
通过 `theme` 指定主题，分为 `light` 和 `dark` 两种。




```vue
<template>
  <div class="menu-demo">
    <a-menu mode="horizontal" theme="dark" :default-selected-keys="['1']">
      <a-menu-item key="0" :style="{ padding: 0, marginRight: '38px' }" disabled>
        <div
          :style="{
            width: '80px',
            height: '30px',
            background: 'var(--color-fill-3)',
            cursor: 'text',
          }"
        />
      </a-menu-item>
      <a-menu-item key="1">Home</a-menu-item>
      <a-menu-item key="2">Solution</a-menu-item>
      <a-menu-item key="3">Cloud Service</a-menu-item>
      <a-menu-item key="4">Cooperation</a-menu-item>
    </a-menu>
  </div>
</template>
<style scoped>
.menu-demo {
  box-sizing: border-box;
  width: 100%;
  padding: 40px;
  background-color: var(--color-neutral-2);
}
</style>
```

## 示例：缩起内嵌菜单

### 说明
通过 `collapsed` 来指定菜单收起。




```vue
<template>
  <div class="menu-demo">
    <a-button
      :style="{ padding: '0 12px', height: '30px', lineHeight: '30px', marginBottom: '4px' }"
      type="primary"
      @click="toggleCollapse"
    >
      <icon-menu-unfold v-if="collapsed" />
      <icon-menu-fold v-else />
    </a-button>
    <a-menu
      :style="{ width: '200px', borderRadius: '4px' }"
      theme="dark"
      :collapsed="collapsed"
      :default-open-keys="['0']"
      :default-selected-keys="['0_2']"
    >
      <a-sub-menu key="0">
        <template #icon><icon-apps></icon-apps></template>
        <template #title>Navigation 1</template>
        <a-menu-item key="0_0">Menu 1</a-menu-item>
        <a-menu-item key="0_1">Menu 2</a-menu-item>
        <a-menu-item key="0_2">Menu 3</a-menu-item>
        <a-menu-item key="0_3">Menu 4</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="1">
        <template #icon><icon-bug></icon-bug></template>
        <template #title>Navigation 2</template>
        <a-menu-item key="1_0">Menu 1</a-menu-item>
        <a-menu-item key="1_1">Menu 2</a-menu-item>
        <a-menu-item key="1_2">Menu 3</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="2">
        <template #icon><icon-bulb></icon-bulb></template>
        <template #title>Navigation 3</template>
        <a-menu-item key="2_0">Menu 1</a-menu-item>
        <a-menu-item key="2_1">Menu 2</a-menu-item>
        <a-sub-menu key="2_2" title="Navigation 4">
          <a-menu-item key="2_2_0">Menu 1</a-menu-item>
          <a-menu-item key="2_2_1">Menu 2</a-menu-item>
        </a-sub-menu>
      </a-sub-menu>
    </a-menu>
  </div>
</template>
<script>
import { ref } from 'vue';
import {
  IconMenuFold,
  IconMenuUnfold,
  IconApps,
  IconBug,
  IconBulb,
} from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconMenuFold,
    IconMenuUnfold,
    IconApps,
    IconBug,
    IconBulb,
  },
  setup() {
    const collapsed = ref(false);
    return {
      collapsed,
      toggleCollapse: () => { collapsed.value = !collapsed.value; },
    }
  }
};
</script>
<style scoped>
.menu-demo {
  box-sizing: border-box;
  width: 100%;
  padding: 40px;
  background-color: var(--color-neutral-2);
}
</style>
```

## 示例：响应式收缩

### 说明
设置 `breakpoint` 可触发响应式收缩。




```vue
<template>
  <div class="menu-demo">
    <a-menu
      :style="{ width: '200px', height: '100%' }"
      :default-open-keys="['0']"
      :default-selected-keys="['0_2']"
      show-collapse-button
      breakpoint="xl"
      @collapse="onCollapse"
    >
      <a-sub-menu key="0">
        <template #icon><icon-apps></icon-apps></template>
        <template #title>Navigation 1</template>
        <a-menu-item key="0_0">Menu 1</a-menu-item>
        <a-menu-item key="0_1">Menu 2</a-menu-item>
        <a-menu-item key="0_2">Menu 3</a-menu-item>
        <a-menu-item key="0_3">Menu 4</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="1">
        <template #icon><icon-bug></icon-bug></template>
        <template #title>Navigation 2</template>
        <a-menu-item key="1_0">Menu 1</a-menu-item>
        <a-menu-item key="1_1">Menu 2</a-menu-item>
        <a-menu-item key="1_2">Menu 3</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="2">
        <template #icon><icon-bulb></icon-bulb></template>
        <template #title>Navigation 3</template>
        <a-menu-item key="2_0">Menu 1</a-menu-item>
        <a-menu-item key="2_1">Menu 2</a-menu-item>
        <a-sub-menu key="2_2" title="Navigation 4">
          <a-menu-item key="2_2_0">Menu 1</a-menu-item>
          <a-menu-item key="2_2_1">Menu 2</a-menu-item>
        </a-sub-menu>
      </a-sub-menu>
    </a-menu>
  </div>
</template>
<script>
import { ref } from 'vue';
import { Message } from '@arco-design/web-vue';
import {
  IconMenuFold,
  IconMenuUnfold,
  IconApps,
  IconBug,
  IconBulb,
} from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconMenuFold,
    IconMenuUnfold,
    IconApps,
    IconBug,
    IconBulb,
  },
  setup() {
    return {
      onCollapse(val, type) {
        const content = type === 'responsive' ? '触发响应式收缩' : '点击触发收缩';
        Message.info({
          content,
          duration: 2000,
        });
      }
    };
  }
};
</script>
<style scoped>
.menu-demo {
  box-sizing: border-box;
  width: 100%;
  height: 600px;
  padding: 40px;
  background-color: var(--color-neutral-2);
}
</style>
```

## 示例：内嵌菜单

### 说明
菜单内可以嵌入多个子项，通过 `openKeys` 可以设置默认打开的子项。




```vue
<template>
  <div class="menu-demo">
    <a-menu
      :style="{ width: '200px', height: '100%' }"
      :default-open-keys="['0']"
      :default-selected-keys="['0_1']"
      show-collapse-button
    >
    <a-menu-item key="0_0_0" data-obj="1">Menu 1</a-menu-item>
      <a-sub-menu key="0">
        <template #icon><icon-apps></icon-apps></template>
        <template #title>Navigation 1</template>
        <a-menu-item key="0_0">Menu 1</a-menu-item>
        <a-menu-item key="0_1">Menu 2</a-menu-item>
        <a-menu-item key="0_2" disabled>Menu 3</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="1">
        <template #icon><icon-bug></icon-bug></template>
        <template #title>Navigation 2</template>
        <a-menu-item key="1_0">Menu 1</a-menu-item>
        <a-menu-item key="1_1">Menu 2</a-menu-item>
        <a-menu-item key="1_2">Menu 3</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="2">
        <template #icon><icon-bulb></icon-bulb></template>
        <template #title>Navigation 3</template>
        <a-menu-item-group title="Menu Group 1">
          <a-menu-item key="2_0">Menu 1</a-menu-item>
          <a-menu-item key="2_1">Menu 2</a-menu-item>
        </a-menu-item-group>
        <a-menu-item-group title="Menu Group 2">
          <a-menu-item key="2_2">Menu 3</a-menu-item>
          <a-menu-item key="2_3">Menu 4</a-menu-item>
        </a-menu-item-group>
      </a-sub-menu>
    </a-menu>
  </div>
</template>
<script>
import {
  IconMenuFold,
  IconMenuUnfold,
  IconApps,
  IconBug,
  IconBulb,
} from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconMenuFold,
    IconMenuUnfold,
    IconApps,
    IconBug,
    IconBulb,
  },
};
</script>
<style scoped>
.menu-demo {
  box-sizing: border-box;
  width: 100%;
  height: 600px;
  padding: 40px;
  background-color: var(--color-neutral-2);
}
</style>
```

## 示例：不同大小菜单

### 说明
通过 `style` 自由指定菜单的宽度和菜单项的高度。




```vue
<template>
  <div class="menu-demo">
    <a-slider
      :style="{ width: '320px', marginBottom: '24px' }"
      v-model="width"
      :step="10"
      :min="160"
      :max="400"
    />
    <a-menu
      showCollapseButton
      :default-open-keys="['0']"
      :default-selected-keys="['0_1']"
      :style="{ width: `${width}px`, height: 'calc(100% - 28px)' }"
    >
      <a-sub-menu key="0">
        <template #icon><IconApps></IconApps></template>
        <template #title>Navigation 1</template>
        <a-menu-item key="0_0">Menu 1</a-menu-item>
        <a-menu-item key="0_1">Menu 2</a-menu-item>
        <a-menu-item key="0_2" disabled>
          Menu 3
        </a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="1">
        <template #icon><IconBug></IconBug></template>
        <template #title>Navigation 2</template>
        <a-menu-item key="1_0">Menu 1</a-menu-item>
        <a-menu-item key="1_1">Menu 2</a-menu-item>
        <a-menu-item key="1_2">Menu 3</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="2">
        <template #icon><IconBulb></IconBulb></template>
        <template #title>Navigation 3</template>
        <a-menu-item key="2_0">Menu 1</a-menu-item>
        <a-menu-item key="2_1">Menu 2</a-menu-item>
        <a-menu-item key="2_2">Menu 3</a-menu-item>
      </a-sub-menu>
    </a-menu>
  </div>
</template>
<script>
import {
  IconMenuFold,
  IconMenuUnfold,
  IconApps,
  IconBug,
  IconBulb,
} from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconMenuFold,
    IconMenuUnfold,
    IconApps,
    IconBug,
    IconBulb,
  },
  data() {
    return {
      width: 240
    }
  }
};
</script>
<style scoped>
.menu-demo {
  box-sizing: border-box;
  width: 100%;
  height: 600px;
  padding: 40px;
  background-color: var(--color-neutral-2);
}
</style>
```

## 示例：悬浮菜单

### 说明
指定 `mode` 为 `pop` 可以使用悬浮菜单。




```vue
<template>
  <div class="menu-demo">
    <a-menu mode="pop" showCollapseButton>
      <a-menu-item key="1">
        <template #icon><icon-apps></icon-apps></template>
        Navigation 1
      </a-menu-item>
      <a-sub-menu key="2">
        <template #icon><icon-bug></icon-bug></template>
        <template #title>Navigation 2</template>
        <a-menu-item key="2_0">Beijing</a-menu-item>
        <a-menu-item key="2_1">Shanghai</a-menu-item>
        <a-menu-item key="2_2">Guangzhou</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="3">
        <template #icon><icon-bulb></icon-bulb></template>
        <template #title>Navigation 3</template>
        <a-menu-item key="3_0">Wuhan</a-menu-item>
        <a-menu-item key="3_1">Chengdu</a-menu-item>
      </a-sub-menu>
      <a-menu-item key="4">
        <template #icon><icon-safe></icon-safe></template>
        Navigation 4
      </a-menu-item>
      <a-menu-item key="5">
        <template #icon><icon-fire></icon-fire></template>
        Navigation 5
      </a-menu-item>
    </a-menu>
  </div>
</template>
<script>
import {
  IconApps,
  IconBug,
  IconBulb,
} from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconApps,
    IconBug,
    IconBulb,
  },
};
</script>
<style scoped>
.menu-demo {
  width: 100%;
  height: 600px;
  padding: 40px;
  box-sizing: border-box;
  background-color: var(--color-neutral-2);
}

.menu-demo .arco-menu {
  width: 200px;
  height: 100%;
  box-shadow: 0 0 1px rgba(0, 0, 0, 0.3);
}

.menu-demo .arco-menu :deep(.arco-menu-collapse-button) {
  width: 32px;
  height: 32px;
  border-radius: 50%;
}

.menu-demo .arco-menu:not(.arco-menu-collapsed) :deep(.arco-menu-collapse-button) {
  right: 0;
  bottom: 8px;
  transform: translateX(50%);
}

.menu-demo .arco-menu:not(.arco-menu-collapsed)::before {
  content: '';
  position: absolute;
  right: 0;
  bottom: 0;
  width: 48px;
  height: 48px;
  background-color: inherit;
  border-radius: 50%;
  box-shadow: -4px 0 2px var(--color-bg-2), 0 0 1px rgba(0, 0, 0, 0.3);
  transform: translateX(50%);
}

.menu-demo .arco-menu.arco-menu-collapsed {
  width: 48px;
  height: auto;
  padding-top: 24px;
  padding-bottom: 138px;
  border-radius: 22px;
}

.menu-demo .arco-menu.arco-menu-collapsed :deep(.arco-menu-collapse-button) {
  right: 8px;
  bottom: 8px;
}
</style>
```

## 示例：悬浮按钮菜单

### 说明
指定 `mode` 为 `popButton` 使用按钮组样式的悬浮菜单。




```vue
<template>
  <div class="menu-demo">
    <a-trigger
      :trigger="['click', 'hover']"
      clickToClose
      position="top"
      v-model:popupVisible="popupVisible1"
    >
      <div :class="`button-trigger ${popupVisible1 ? 'button-trigger-active' : ''}`">
        <IconClose v-if="popupVisible1" />
        <IconMessage v-else />
      </div>
      <template #content>
        <a-menu
          :style="{ marginBottom: '-4px' }"
          mode="popButton"
          :tooltipProps="{ position: 'left' }"
          showCollapseButton
        >
          <a-menu-item key="1">
            <template #icon><IconBug></IconBug></template>
            Bugs
          </a-menu-item>
          <a-menu-item key="2">
            <template #icon><IconBulb></IconBulb></template>
            Ideas
          </a-menu-item>
        </a-menu>
      </template>
    </a-trigger>

    <a-trigger
      :trigger="['click', 'hover']"
      clickToClose
      position="top"
      v-model:popupVisible="popupVisible2"
    >
      <div :class="`button-trigger ${popupVisible2 ? 'button-trigger-active' : ''}`">
        <IconClose v-if="popupVisible2" />
        <IconMessage v-else />
      </div>
      <template #content>
        <a-menu
          :style="{ marginBottom: '-4px' }"
          mode="popButton"
          :tooltipProps="{ position: 'left' }"
          showCollapseButton
        >
          <a-menu-item key="1">
            <template #icon><IconBug></IconBug></template>
            Bugs
          </a-menu-item>
          <a-menu-item key="2">
            <template #icon><IconBulb></IconBulb></template>
            Ideas
          </a-menu-item>
        </a-menu>
      </template>
    </a-trigger>
  </div>
</template>
<script>
import {
  IconBug,
  IconBulb,
  IconClose,
  IconMessage,
} from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconBug,
    IconBulb,
    IconClose,
    IconMessage,
  },
  data() {
    return {
      popupVisible1: false,
      popupVisible2: false,
    };
  }
};
</script>
<style scoped>
.menu-demo {
  box-sizing: border-box;
  width: 660px;
  height: 300px;
  padding: 40px;
  background-color: var(--color-fill-2);
  position: relative;
}
.button-trigger {
  position: absolute;
  bottom: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  color: var(--color-white);
  font-size: 14px;
  border-radius: 50%;
  cursor: pointer;
  transition: all 0.1s;
}
/* button left */
.button-trigger:nth-child(1) {
  left: 150px;
  background-color: var(--color-neutral-5);
}
.button-trigger:nth-child(1).button-trigger-active {
  background-color: var(--color-neutral-4);
}
/* button right */
.button-trigger:nth-child(2) {
  left: 372px;
  background-color: rgb(var(--arcoblue-6));
}
.button-trigger:nth-child(3).button-trigger-active {
  background-color: var(--color-primary-light-4);
}
</style>
```

## API


### `<menu>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|theme|菜单的主题|`'light' \| 'dark'`|`'light'`||
|mode|菜单的模式|`'vertical' \| 'horizontal' \| 'pop' \| 'popButton'`|`'vertical'`||
|level-indent|层级之间的缩进量|`number`|`-`||
|auto-open|默认展开所有多级菜单|`boolean`|`false`||
|collapsed **(v-model)**|是否折叠菜单|`boolean`|`-`||
|default-collapsed|默认是否折叠菜单|`boolean`|`false`||
|collapsed-width|折叠菜单宽度|`number`|`-`||
|accordion|开启手风琴效果|`boolean`|`false`||
|auto-scroll-into-view|是否自动滚动选中项目到可见区域|`boolean`|`false`||
|show-collapse-button|是否内置折叠按钮|`boolean`|`false`||
|selected-keys **(v-model)**|选中的菜单项 key 数组|`string[]`|`-`||
|default-selected-keys|默认选中的菜单项 key 数组|`string[]`|`[]`||
|open-keys **(v-model)**|展开的子菜单 key 数组|`string[]`|`-`||
|default-open-keys|默认展开的子菜单 key 数组|`string[]`|`[]`||
|scroll-config|滚动到可见区域的配置项，接收所有[scroll-into-view-if-needed](https://github.com/stipsan/scroll-into-view-if-needed)的参数|`{ [key: string]: any }`|`-`||
|trigger-props|弹出模式下可接受所有 `Trigger` 的 `Props`|`TriggerProps`|`-`||
|tooltip-props|弹出模式下可接受所有 `ToolTip` 的 `Props`|`object`|`-`||
|auto-open-selected|默认展开选中的菜单|`boolean`|`false`|2.8.0|
|breakpoint|响应式的断点, 详见[响应式栅格](/vue/component/grid)|`'xxl' \| 'xl' \| 'lg' \| 'md' \| 'sm' \| 'xs'`|`-`|2.18.0|
|popup-max-height|弹出框的最大高度|`boolean \| number`|`true`|2.23.0|
### `<menu>` 事件

|事件名|描述|参数|
|---|---|---|
|collapse|折叠状态改变时触发|collapsed: `boolean`<br>type: `'clickTrigger'\|'responsive'`|
|menu-item-click|点击菜单项时触发|key: `string`|
|sub-menu-click|点击子菜单时触发|key: `string`<br>openKeys: `string[]`|
### `<menu>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|collapse-icon|折叠图标|collapsed: `boolean`|
|expand-icon-right|向右展开的图标|-|
|expand-icon-down|向下展开的图标|-|




### `<sub-menu>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|title|子菜单的标题|`string`|`-`||
|selectable|弹出模式下，是否将多级菜单头也作为一个菜单项，支持点击选中等状态|`boolean`|`false`||
|popup|是否强制使用弹出模式，`level` 表示当前子菜单的层级|`boolean \| ((level: number) => boolean)`|`false`||
|popup-max-height|弹出框的最大高度|`boolean \| number`|`true`|2.23.0|
### `<sub-menu>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|title|标题|-||
|expand-icon-right|向右展开的图标|-||
|expand-icon-down|向下展开的图标|-||
|icon|菜单的图标|-|2.11.0|




### `<menu-item-group>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|title|菜单组的标题|`string`|`-`|
### `<menu-item-group>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|title|标题|-|




### `<menu-item>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|disabled|是否禁用|`boolean`|`false`|
### `<menu-item>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|icon|菜单的图标|-|2.11.0|




## FAQ

### `<MenuItem>` 和 `<SubMenu>` 组件的 `key` 属性为必填
在 `<Menu>` 组件中使用 `<MenuItem>` 和 `<SubMenu>` 组件时，请传入唯一的 `key` 属性。
组件内部在进行计算时会依赖此值，如果没有赋值会导致部分场景下异常
