---
name: arco-vue-drawer
description: "Arco Design Vue 抽屉 Drawer 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-drawer>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 抽屉 Drawer

来源组件：上游 `web-vue/components/drawer`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-drawer>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
点击触发按钮抽屉从右侧滑出，点击遮罩区关闭。




```vue
<template>
  <a-button type="primary" @click="handleClick">Open Drawer</a-button>
  <a-drawer :width="340" :visible="visible" @ok="handleOk" @cancel="handleCancel" unmountOnClose>
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you
      press the OK button.
    </div>
  </a-drawer>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visible = ref(false);

    const handleClick = () => {
      visible.value = true;
    };
    const handleOk = () => {
      visible.value = false;
    };
    const handleCancel = () => {
      visible.value = false;
    }

    return {
      visible,
      handleClick,
      handleOk,
      handleCancel
    }
  },
};
</script>
```

## 示例：抽屉位置

### 说明
自定义位置，点击触发按钮抽屉从相应的位置滑出。




```vue
<template>
  <a-radio-group v-model="position">
    <a-radio value="top">Top</a-radio>
    <a-radio value="right">Right</a-radio>
    <a-radio value="bottom">Bottom</a-radio>
    <a-radio value="left">Left</a-radio>
  </a-radio-group>
  <div :style="{marginTop: '20px'}">
    <a-button type="primary" @click="handleClick">Open Drawer</a-button>
  </div>
  <a-drawer
    :width="340"
    :height="340"
    :visible="visible"
    :placement="position"
    @ok="handleOk"
    @cancel="handleCancel"
    unmountOnClose
  >
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you press the OK button.</div>
  </a-drawer>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visible = ref(false);
    const position = ref('right');

    const handleClick = () => {
      visible.value = true;
    };
    const handleOk = () => {
      visible.value = false;
    };
    const handleCancel = () => {
      visible.value = false;
    }

    return {
      visible,
      position,
      handleClick,
      handleOk,
      handleCancel
    }
  },
};
</script>
```

## 示例：自定义节点

### 说明
通过插槽自定义内容，或者设置相应属性来控制显示或隐藏。




```vue
<template>
  <a-checkbox-group v-model="custom" :options="['hide header', 'hide footer', 'hide cancel']"/>
  <div :style="{marginTop: '20px'}">
    <a-button type="primary" @click="handleClick">Open Drawer</a-button>
  </div>
  <a-drawer
    :width="340"
    :header="!custom.includes('hide header')"
    :footer="!custom.includes('hide footer')"
    :hide-cancel="custom.includes('hide cancel')"
    :visible="visible"
    @ok="handleOk"
    @cancel="handleCancel"
    unmountOnClose
  >
    <template #header>
      <span>Header and title</span>
    </template>
    <div>
      You can customize modal body text by the current situation. This modal will be closed immediately once you
      press the OK button.
    </div>
  </a-drawer>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visible = ref(false);
    const custom = ref([])

    const handleClick = () => {
      visible.value = true;
    };
    const handleOk = () => {
      visible.value = false;
    };
    const handleCancel = () => {
      visible.value = false;
    }

    return {
      custom,
      visible,
      handleClick,
      handleOk,
      handleCancel
    }
  },
};
</script>
```

## 示例：嵌套抽屉

### 说明
在抽屉内打开新的抽屉。




```vue
<template>
  <a-button type="primary" @click="handleClick">Open Drawer</a-button>
  <a-drawer :visible="visible" :width="500" @ok="handleOk" @cancel="handleCancel" unmountOnClose>
    <template #title>
      Title
    </template>
    <div :style="{marginBottom: '20px'}">You can customize modal body text by the current situation. This modal will be closed immediately once you press the OK button.</div>
    <a-button type="primary" @click="handleNestedClick">Open Nested Drawer</a-button>
  </a-drawer>
  <a-drawer :visible="nestedVisible" @ok="handleNestedOk" @cancel="handleNestedCancel" unmountOnClose>
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you press the OK button.</div>
  </a-drawer>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visible = ref(false);
    const nestedVisible = ref(false);

    const handleClick = () => {
      visible.value = true;
    };
    const handleOk = () => {
      visible.value = false;
    };
    const handleCancel = () => {
      visible.value = false;
    }
    const handleNestedClick = () => {
      nestedVisible.value = true;
    };
    const handleNestedOk = () => {
      nestedVisible.value = false;
    };
    const handleNestedCancel = () => {
      nestedVisible.value = false;
    }

    return {
      visible,
      nestedVisible,
      handleClick,
      handleOk,
      handleCancel,
      handleNestedClick,
      handleNestedOk,
      handleNestedCancel
    }
  },
};
</script>
```

## 示例：挂载位置

### 说明
通过 `popup-container` 可以设置弹出层节点的挂载位置




```vue
<template>
  <div>
    <div
      id="parentNode"
      style="width: 100%; height: 300px; background-color: var(--color-fill-2); position: relative; overflow: hidden; line-height: 300px; text-align: center;"
    >
      <a-button type="primary" @click="handleClick">Open Drawer</a-button>
    </div>
  </div>
  <a-drawer
    popup-container="#parentNode"
    :visible="visible"
    @ok="handleOk"
    @cancel="handleCancel"
  >
    <template #title> Title </template>
    <div
      >You can customize modal body text by the current situation. This modal
      will be closed immediately once you press the OK button.</div
    >
  </a-drawer>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visible = ref(false);

    const handleClick = () => {
      visible.value = true;
    };
    const handleOk = () => {
      visible.value = false;
    };
    const handleCancel = () => {
      visible.value = false;
    }

    return {
      visible,
      handleClick,
      handleOk,
      handleCancel
    }
  },
};
</script>
```

## 示例：函数调用

### 说明
通过函数的方式使用抽屉。




```vue
<template>
  <a-button type="primary" @click="handleClick">Open Drawer</a-button>
</template>

<script>
import { Drawer } from '@arco-design/web-vue';

export default {
  setup() {
    const handleClick = () => {
      Drawer.open({
        title: 'Info Title',
        content: 'This is an info message',
        width: 340
      });
    };

    return {
      handleClick,
    }
  },
}
</script>
```

## API


### `<drawer>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|visible **(v-model)**|抽屉是否可见|`boolean`|`false`||
|default-visible|抽屉默认是否可见（非受控模式）|`boolean`|`false`||
|placement|抽屉放置的位置|`'top' \| 'right' \| 'bottom' \| 'left'`|`'right'`||
|title|标题|`string`|`-`||
|mask|是否显示遮罩层|`boolean`|`true`||
|mask-closable|点击遮罩层是否可以关闭|`boolean`|`true`||
|closable|是否展示关闭按钮|`boolean`|`true`||
|ok-text|确认按钮的内容|`string`|`-`||
|cancel-text|取消按钮的内容|`string`|`-`||
|ok-loading|确认按钮是否为加载中状态|`boolean`|`false`||
|ok-button-props|确认按钮的Props|`ButtonProps`|`-`|2.9.0|
|cancel-button-props|取消按钮的Props|`ButtonProps`|`-`|2.9.0|
|unmount-on-close|关闭时是否卸载节点|`boolean`|`false`|2.12.0|
|width|抽屉的宽度（仅在placement为right,left时可用）|`number\|string`|`250`||
|height|抽屉的高度（仅在placement为top,bottom时可用）|`number\|string`|`250`||
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`'body'`||
|drawer-style|抽屉的样式|`CSSProperties`|`-`||
|body-class|抽屉内容部分的类名|`string \| any[]`|`-`|2.57.0|
|body-style|抽屉内容部分的样式|`StyleValue`|`-`|2.57.0|
|on-before-ok|触发 ok 事件前的回调函数。如果返回 false 则不会触发后续事件，也可使用 done 进行异步关闭。|`(  done: (closed: boolean) => void) => void \| boolean \| Promise<void \| boolean>`|`-`||
|on-before-cancel|触发 cancel 事件前的回调函数。如果返回 false 则不会触发后续事件。|`() => boolean`|`-`||
|esc-to-close|是否支持 ESC 键关闭抽屉|`boolean`|`true`|2.15.0|
|render-to-body|抽屉是否挂载在 `body` 元素下|`boolean`|`true`||
|header|是否展示头部内容|`boolean`|`true`|2.33.0|
|footer|是否展示底部内容|`boolean`|`true`|2.11.0|
|hide-cancel|是否隐藏取消按钮|`boolean`|`false`|2.19.0|
### `<drawer>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|ok|点击确定按钮时触发|ev: `MouseEvent`||
|cancel|点击取消、关闭按钮时触发|ev: `MouseEvent \| KeyboardEvent`||
|open|抽屉打开后（动画结束）触发|-||
|close|抽屉关闭后（动画结束）触发|-||
|before-open|对话框打开前触发|-|2.43.0|
|before-close|对话框关闭前触发|-|2.43.0|
### `<drawer>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|header|页眉|-|2.33.0|
|title|标题|-||
|footer|页脚|-||



### `<drawer>` 全局方法

Drawer 提供的全局方法，可以通过以下三种方法使用：

1. 通过 `this.$drawer` 调用
2. 在 Composition API 中，通过 `getCurrentInstance().appContext.config.globalProperties.$drawer` 调用
3. 导入 Drawer，通过 Drawer 本身调用

当通过 import 方式使用时，组件没有办法获取当前的 Vue Context，如 i18n 或 route 等注入在 AppContext 上的内容无法在内部使用，需要在调用时手动传入 AppContext，或者为组件全局指定 AppContext

```ts
import { createApp } from 'vue'
import { Drawer } from '@arco-design/web-vue';

const app = createApp(App);
Drawer._context = app._context;
```


### DrawerConfig

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|placement|抽屉放置的位置|`'top' \| 'right' \| 'bottom' \| 'left'`|`'right'`||
|title|标题|`RenderContent`|`-`||
|content|内容|`RenderContent`|`-`||
|mask|是否显示遮罩层|`boolean`|`true`||
|maskClosable|点击遮罩层是否可以关闭|`boolean`|`true`||
|closable|是否展示关闭按钮|`boolean`|`true`||
|okText|确认按钮的内容|`string`|`-`||
|cancelText|取消按钮的内容|`string`|`-`||
|okLoading|确认按钮是否为加载中状态|`boolean`|`false`||
|okButtonProps|确认按钮的Props|`ButtonProps`|`-`|2.9.0|
|cancelButtonProps|取消按钮的Props|`ButtonProps`|`-`|2.9.0|
|width|抽屉的宽度（仅在placement为right,left时可用）|`number \| string`|`250`||
|height|抽屉的高度（仅在placement为top,bottom时可用）|`number \| string`|`250`||
|popupContainer|弹出框的挂载容器|`string \| HTMLElement`|`'body'`||
|drawerStyle|抽屉的样式|`CSSProperties`|`-`||
|onOk|点击确定按钮时触发|`(e?: Event) => void`|`-`||
|onCancel|点击取消、关闭按钮时触发|`(e?: Event) => void`|`-`||
|onBeforeOk|触发 ok 事件前的回调函数。如果返回 false 则不会触发后续事件，也可使用 done 进行异步关闭。|`(    done: (closed: boolean) => void  ) => void \| boolean \| Promise<void \| boolean>`|`-`||
|onBeforeCancel|触发 cancel 事件前的回调函数。如果返回 false 则不会触发后续事件。|`() => boolean`|`-`||
|onOpen|抽屉打开后（动画结束）触发|`() => void`|`-`||
|onClose|抽屉关闭后（动画结束）触发|`() => void`|`-`||
|onBeforeOpen|抽屉打开前触发|`() => void`|`-`|2.43.0|
|onBeforeClose|抽屉关闭前触发|`() => void`|`-`|2.43.0|
|escToClose|是否支持 ESC 键关闭抽屉|`boolean`|`true`|2.15.0|
|header|是否展示头部内容|`boolean \| RenderContent`|`true`|2.33.0|
|footer|是否展示底部内容|`boolean \| RenderContent`|`true`|2.11.0|
|hideCancel|是否隐藏取消按钮|`boolean`|`false`|2.19.0|



### DrawerReturn

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|close|关闭抽屉|`() => void`|`-`||
|update|更新抽屉|`(config: DrawerUpdateConfig) => void`|`-`|2.43.2|



### DrawerMethod

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|open|打开抽屉|`(config: DrawerConfig, appContext?: AppContext) => DrawerReturn`|`-`|
