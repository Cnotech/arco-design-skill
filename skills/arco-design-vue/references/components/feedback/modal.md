---
name: arco-vue-modal
description: "Arco Design Vue Modal 对话框 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-modal>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# Modal 对话框

来源组件：上游 `web-vue/components/modal`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-modal>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
对话框的基本用法。




```vue
<template>
  <a-button @click="handleClick">Open Modal</a-button>
  <a-modal v-model:visible="visible" @ok="handleOk" @cancel="handleCancel">
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you press the OK button.</div>
  </a-modal>
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
}
</script>
```

## 示例：异步关闭

### 说明
可以通过 on-before-ok 更简洁的实现异步关闭功能




```vue

<template>
  <a-button @click="handleClick">Open Modal</a-button>
  <a-modal v-model:visible="visible" @cancel="handleCancel" :on-before-ok="handleBeforeOk" unmountOnClose>
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you
      press the OK button.
    </div>
  </a-modal>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visible = ref(false);

    const handleClick = () => {
      visible.value = true;
    };
    const handleBeforeOk = async () => {
      await new Promise(resolve => setTimeout(resolve, 3000));
      return true;
      // prevent close
      // return false;
    };
    const handleCancel = () => {
      visible.value = false;
    }

    return {
      visible,
      handleClick,
      handleBeforeOk,
      handleCancel
    }
  },
}
</script>
```

## 示例：函数调用

### 说明
通过函数的方式使用对话框。




```vue
<template>
  <a-button @click="handleClick">Open Modal</a-button>
</template>

<script>
import { h } from 'vue';
import { Modal, Button } from '@arco-design/web-vue';

const ModalContent = {
  setup() {
    const onClick = () => {
      Modal.info({
        title: 'Info Title',
        content: 'This is an nest info message'
      });
    };

    return () => h('div', {class: 'info-modal-content'}, [
      h('span', {style: 'margin-bottom: 10px;'}, 'This is an info message'),
      h(Button, {size: 'mini', onClick}, 'Open Nest Modal')
    ])
  },
}

export default {
  setup() {
    const handleClick = () => {
      Modal.info({
        title: 'Info Title',
        content: () => h(ModalContent)
      });
    };

    return {
      handleClick
    }
  },
}
</script>

<style>
.info-modal-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
```

## 示例：消息提示

### 说明
有**info**, **success**, **warning**, **error**四种类型的消息提示，仅提供一个确认按钮用于关闭消息提示对话框。
消息默认会默认开启 `simple` 和 `hideCancel`，如果想要取消可以再次设置。




```vue
<template>
  <a-space>
    <a-button @click="handleClickInfo">Info</a-button>
    <a-button @click="handleClickSuccess" status="success">Success</a-button>
    <a-button @click="handleClickWarning" status="warning">Warning</a-button>
    <a-button @click="handleClickError" status="danger">Error</a-button>
  </a-space>
</template>

<script>
import { Modal } from '@arco-design/web-vue';

export default {
  setup() {
    const handleClickInfo = () => {
      Modal.info({
        title: 'Info Notification',
        content: 'This is an info description which directly indicates a neutral informative change or action.'
      });
    };
    const handleClickSuccess = () => {
      Modal.success({
        title: 'Success Notification',
        content: 'This is a success notification'
      });
    };
    const handleClickWarning = () => {
      Modal.warning({
        title: 'Warning Notification',
        content: 'This is a warning description which directly indicates a warning that might need attention.'
      });
    };
    const handleClickError = () => {
      Modal.error({
        title: 'Error Notification',
        content: 'This is an error description which directly indicates a dangerous or potentially negative action.'
      });
    };

    return {
      handleClickInfo,
      handleClickSuccess,
      handleClickWarning,
      handleClickError
    }
  },
}
</script>
```

## 示例：对话框的宽度

### 说明
设置 `width="auto"` 可以让对话框自适应宽度




```vue
<template>
  <a-button @click="handleClick">Open Modal</a-button>
  <a-modal width="auto" v-model:visible="visible" @ok="handleOk" @cancel="handleCancel">
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you press the OK button.</div>
  </a-modal>
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
}
</script>
```

## 示例：定制按钮文字

### 说明
设置 `okText` 与 `cancelText` 可以自定义按钮文字。




```vue
<template>
  <a-button @click="handleClick">Open Modal</a-button>
  <a-modal :visible="visible" @ok="handleOk" @cancel="handleCancel" okText="Confirm" cancelText="Exit" unmountOnClose>
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you press the OK button.</div>
  </a-modal>
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
}
</script>
```

## 示例：弹出层表单

### 说明
在对话框中使用表单




```vue

<template>
  <a-button @click="handleClick">Open Form Modal</a-button>
  <a-modal v-model:visible="visible" title="Modal Form" @cancel="handleCancel" @before-ok="handleBeforeOk">
    <a-form :model="form">
      <a-form-item field="name" label="Name">
        <a-input v-model="form.name" />
      </a-form-item>
      <a-form-item field="post" label="Post">
        <a-select v-model="form.post">
          <a-option value="post1">Post1</a-option>
          <a-option value="post2">Post2</a-option>
          <a-option value="post3">Post3</a-option>
          <a-option value="post4">Post4</a-option>
        </a-select>
      </a-form-item>
    </a-form>
  </a-modal>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const visible = ref(false);
    const form = reactive({
      name: '',
      post: ''
    });

    const handleClick = () => {
      visible.value = true;
    };
    const handleBeforeOk = (done) => {
      console.log(form)
      window.setTimeout(() => {
        done()
        // prevent close
        // done(false)
      }, 3000)
    };
    const handleCancel = () => {
      visible.value = false;
    }

    return {
      visible,
      form,
      handleClick,
      handleBeforeOk,
      handleCancel
    }
  },
}
</script>
```

## 示例：可拖动

### 说明
开启 `draggable` 属性，允许用户拖动对话框。




```vue
<template>
  <a-button @click="handleClick">Open Draggable Modal</a-button>
  <a-modal v-model:visible="visible" @ok="handleOk" @cancel="handleCancel" draggable>
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you press the OK button.</div>
  </a-modal>
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
}
</script>
```

## 示例：全屏

### 说明
开启 `fullscreen` 属性，可以让对话框占满整个容器。




```vue
<template>
  <a-button @click="handleClick">Open Modal</a-button>
  <a-modal v-model:visible="visible" @ok="handleOk" @cancel="handleCancel" fullscreen>
    <template #title>
      Title
    </template>
    <div>You can customize modal body text by the current situation. This modal will be closed immediately once you press the OK button.</div>
  </a-modal>
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
}
</script>
```

## API


### `<modal>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|visible **(v-model)**|对话框是否可见|`boolean`|`-`||
|default-visible|对话框默认是否可见（非受控状态）|`boolean`|`false`||
|width|对话框的宽度，不设置的情况下会使用样式中的宽度值|`number\|string`|`-`|2.12.0|
|top|对话框的距离顶部的高度，居中显示开启的情况下不生效|`number\|string`|`-`|2.12.0|
|mask|是否显示遮罩层|`boolean`|`true`||
|title|标题|`string`|`-`||
|title-align|标题的水平对齐方向|`'start' \| 'center'`|`'center'`|2.17.0|
|align-center|对话框是否居中显示|`boolean`|`true`||
|unmount-on-close|关闭时是否卸载节点|`boolean`|`false`||
|mask-closable|是否点击遮罩层可以关闭对话框|`boolean`|`true`||
|hide-cancel|是否隐藏取消按钮|`boolean`|`false`||
|simple|是否开启简单模式|`boolean`|`(props: any) => {  return props.notice;}`||
|closable|是否显示关闭按钮|`boolean`|`true`||
|ok-text|确认按钮的内容|`string`|`-`||
|cancel-text|取消按钮的内容|`string`|`-`||
|ok-loading|确认按钮是否为加载中状态|`boolean`|`false`||
|ok-button-props|确认按钮的Props|`ButtonProps`|`-`||
|cancel-button-props|取消按钮的Props|`ButtonProps`|`-`||
|footer|是否展示页脚部分|`boolean`|`true`||
|render-to-body|对话框是否挂载在 `body` 元素下|`boolean`|`true`||
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`'body'`||
|mask-style|蒙层的样式|`CSSProperties`|`-`||
|modal-class|对话框的类名|`string \| any[]`|`-`||
|modal-style|对话框的样式|`CSSProperties`|`-`||
|on-before-ok|触发 ok 事件前的回调函数。如果返回 false 则不会触发后续事件，也可使用 done 进行异步关闭。|`(  done: (closed: boolean) => void) => void \| boolean \| Promise<void \| boolean>`|`-`|2.7.0|
|on-before-cancel|触发 cancel 事件前的回调函数。如果返回 false 则不会触发后续事件。|`() => boolean`|`-`|2.7.0|
|esc-to-close|是否支持 ESC 键关闭对话框|`boolean`|`true`|2.15.0|
|draggable|是否支持拖动|`boolean`|`false`|2.19.0|
|fullscreen|是否开启全屏|`boolean`|`false`|2.19.0|
|mask-animation-name|遮罩层动画名字|`string`|`-`|2.24.0|
|modal-animation-name|对话框动画名字|`string`|`-`|2.24.0|
|body-class|对话框内容部分的类名|`string \| any[]`|`-`|2.31.0|
|body-style|对话框内容部分的样式|`StyleValue`|`-`|2.31.0|
|hide-title|是否隐藏标题|`boolean`|`false`|2.50.0|
### `<modal>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|ok|点击确定按钮时触发|ev: `MouseEvent`||
|cancel|点击取消、关闭按钮时触发|ev: `MouseEvent \| KeyboardEvent`||
|open|对话框打开后（动画结束）触发|-||
|close|对话框关闭后（动画结束）触发|-||
|before-open|对话框打开前触发|-|2.16.0|
|before-close|对话框关闭前触发|-|2.16.0|
### `<modal>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|title|标题|-|
|footer|页脚|-|



### `<modal>` 全局方法

Modal提供的全局方法，可以通过以下三种方法使用：

1. 通过this.$modal调用
2. 在Composition API中，通过getCurrentInstance().appContext.config.globalProperties.$modal调用
3. 导入Modal，通过Modal本身调用

当通过 import 方式使用时，组件没有办法获取当前的 Vue Context，如 i18n 或 route 等注入在 AppContext 上的内容无法在内部使用，需要在调用时手动传入 AppContext，或者为组件全局指定 AppContext

```ts
import { createApp } from 'vue'
import { Modal } from '@arco-design/web-vue';

const app = createApp(App);
Modal._context = app._context;
```


### ModalConfig

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|title|标题|`RenderContent`|`-`||
|content|内容|`RenderContent`|`-`||
|footer|页脚|`boolean \| RenderContent`|`true`||
|closable|是否显示关闭按钮|`boolean`|`true`||
|okText|确认按钮的内容|`string`|`-`||
|cancelText|取消按钮的内容|`string`|`-`||
|okButtonProps|确认按钮的Props|`ButtonProps`|`-`||
|cancelButtonProps|取消按钮的Props|`ButtonProps`|`-`||
|okLoading|确认按钮是否为加载中状态|`boolean`|`false`||
|hideCancel|是否隐藏取消按钮|`boolean`|`false`||
|mask|是否显示遮罩层|`boolean`|`true`||
|simple|是否开启简单模式|`boolean`|`false`||
|maskClosable|是否点击遮罩层可以关闭对话框|`boolean`|`true`||
|maskStyle|蒙层的样式|`CSSProperties`|`-`||
|alignCenter|对话框是否居中显示|`boolean`|`true`||
|escToClose|是否支持 ESC 键关闭对话框|`boolean`|`true`|2.15.0|
|draggable|是否支持拖动|`boolean`|`false`|2.19.0|
|fullscreen|是否开启全屏|`boolean`|`false`|2.19.0|
|onOk|点击确定按钮的回调函数|`(e?: Event) => void`|`-`||
|onCancel|点击取消按钮的回调函数|`(e?: Event) => void`|`-`||
|onBeforeOk|触发 ok 事件前的回调函数。如果返回 false 则不会触发后续事件，也可使用 done 进行异步关闭。|`(    done: (closed: boolean) => void  ) => void \| boolean \| Promise<void \| boolean>`|`-`|2.7.0|
|onBeforeCancel|触发 cancel 事件前的回调函数。如果返回 false 则不会触发后续事件。|`() => boolean`|`-`|2.7.0|
|onOpen|对话框打开后（动画结束）触发|`() => void`|`-`||
|onClose|对话框关闭后（动画结束）触发|`() => void`|`-`||
|onBeforeOpen|对话框打开前触发|`() => void`|`-`|2.16.0|
|onBeforeClose|对话框关闭前触发|`() => void`|`-`|2.16.0|
|width|对话框的宽度，不设置的情况下会使用样式中的宽度值|`number \| string`|`-`|2.12.0|
|top|对话框的距离顶部的高度，居中显示开启的情况下不生效|`number \| string`|`-`|2.12.0|
|titleAlign|标题的水平对齐方向|`'start' \| 'center'`|`'center'`|2.17.0|
|renderToBody|对话框是否挂载在 `body` 元素下|`boolean`|`true`||
|popupContainer|弹出框的挂载容器|`string \| HTMLElement`|`'body'`||
|modalClass|对话框的类名|`string \| any[]`|`-`||
|modalStyle|对话框的样式|`CSSProperties`|`-`||
|maskAnimationName|遮罩层动画名字|`string`|`-`|2.24.0|
|modalAnimationName|对话框动画名字|`string`|`-`|2.24.0|
|hideTitle|是否隐藏标题|`boolean`|`false`|2.50.0|
|bodyClass|对话框内容部分的类名|`string \| any[]`|`-`||
|bodyStyle|对话框内容部分的样式|`StyleValue`|`-`||



### ModalReturn

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|close|关闭对话框|`() => void`|`-`||
|update|更新对话框|`(config: ModalUpdateConfig) => void`|`-`|2.43.2|



### ModalMethod

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|open|打开对话框|`(config: ModalConfig, appContext?: AppContext) => ModalReturn`|`-`|
|confirm|打开对话框（简单模式）|`(config: ModalConfig, appContext?: AppContext) => ModalReturn`|`-`|
|info|打开信息对话框|`(config: ModalConfig, appContext?: AppContext) => ModalReturn`|`-`|
|success|打开成功对话框|`(config: ModalConfig, appContext?: AppContext) => ModalReturn`|`-`|
|warning|打开警告对话框|`(config: ModalConfig, appContext?: AppContext) => ModalReturn`|`-`|
|error|打开错误对话框|`(config: ModalConfig, appContext?: AppContext) => ModalReturn`|`-`|
