---
name: arco-vue-message
description: "Arco Design Vue 全局提示 Message 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-message>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 全局提示 Message

来源组件：上游 `web-vue/components/message`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 使用全局 Message 服务：`this.$message`、`getCurrentInstance().appContext.config.globalProperties.$message`，或从 `@arco-design/web-vue` 导入 `Message`。该 API 不是 `<a-message>` 组件标签。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
全局提示的基本用法。




```vue
<template>
  <a-button @click="handleClick">Info Message</a-button>
</template>

<script>
export default {
  methods: {
    handleClick() {
      this.$message.info('This is an info message')
    }
  }
};
</script>
```

## 示例：消息类型

### 说明
全局提示有 6 种不同的类型，分别为：`info`, `success`, `warning`, `error`, `loading`。2.41.0 版本增加 `normal` 类型，此类型下默认没有图标。




```vue

<template>
  <div>
    <a-space>
      <a-button @click="()=>this.$message.info('This is an info message!')">Info Message</a-button>
      <a-button @click="()=>this.$message.success('This is a success message!')" status="success">Success Message
      </a-button>
      <a-button @click="()=>this.$message.warning('This is a warning message!')" status="warning">Warning Message
      </a-button>
      <a-button @click="()=>this.$message.error('This is an error message!')" status="danger">Error Message</a-button>
    </a-space>
  </div>
  <div style="margin-top: 20px">
    <a-space>
      <a-button @click="()=>this.$message.normal('This is a normal message!')">Normal Message</a-button>
      <a-button @click="()=>this.$message.normal({
    content:'This is a normal message!',
    icon:renderIcon
    })">Normal Message With Icon
      </a-button>
      <a-button @click="()=>this.$message.loading('This is a loading message!')" status="primary">Loading Message
      </a-button>
    </a-space>
  </div>
</template>

<script>
import { h } from 'vue';
import { IconExclamationCircleFill } from '@arco-design/web-vue/es/icon';

export default {
  setup() {
    const renderIcon = () => h(IconExclamationCircleFill);
    return {
      renderIcon
    }
  }
};
</script>
```

## 示例：自定义图标

### 说明
设置 `icon` 来自定义图标。




```vue
<template>
  <a-button @click="handleClick">Info Message</a-button>
</template>

<script>
import { h } from 'vue';
import { IconFaceSmileFill } from '@arco-design/web-vue/es/icon';

export default {
  methods: {
    handleClick() {
      this.$message.info({
        content: 'This is an info message!',
        icon: () => h(IconFaceSmileFill)
      });
    }
  }
}
</script>
```

## 示例：全局提示的位置

### 说明
全局提示有 2 种不同的弹出位置，分别为顶部和底部。




```vue
<template>
  <a-space>
    <a-button @click="()=>this.$message.info({content:'This is an info message!'})">Top Message</a-button>
    <a-button @click="()=>this.$message.info({content:'This is an info message!',position:'bottom'})">Bottom Message</a-button>
  </a-space>
</template>
```

## 示例：可关闭

### 说明
设置 `closable` 来显示关闭按钮。




```vue
<template>
  <a-button @click="handleClick">Closeable Message</a-button>
</template>

<script>
export default {
  methods: {
    handleClick(){
      this.$message.info({
        content:'This is an info message!',
        closable: true
      })
    }
  }
};
</script>
```

## 示例：更新内容

### 说明
更新消息内容，通过设置 `duration` 属性可以重置定时器。




```vue
<template>
  <a-button @click="handleClick">Update Info Message</a-button>
</template>

<script>
export default {
  data() {
    return {
      index: 0
    }
  },
  methods: {
    handleClick() {
      this.$message.info({
        id: 'myInfo',
        content: `This is an info message ${this.$data.index++}`,
        duration: 2000
      })
    }
  }
};
</script>
```

## API

### `Message` 全局方法

Message提供的全局方法，可以通过以下三种方法使用：
1. 通过this.$message调用
2. 在Composition API中，通过getCurrentInstance().appContext.config.globalProperties.$message调用
3. 导入Message，通过Message本身调用

当通过 import 方式使用时，组件没有办法获取当前的 Vue Context，如 i18n 或 route 等注入在 AppContext 上的内容无法在内部使用，需要在调用时手动传入 AppContext，或者为组件全局指定 AppContext

```ts
import { createApp } from 'vue'
import { Message } from '@arco-design/web-vue';

const app = createApp(App);
Message._context = app._context;
```


### MessageMethod

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|info|显示信息提示|`(    config: string \| MessageConfig,    appContext?: AppContext  ) => MessageReturn`|`-`||
|success|显示成功提示|`(    config: string \| MessageConfig,    appContext?: AppContext  ) => MessageReturn`|`-`||
|warning|显示警告提示|`(    config: string \| MessageConfig,    appContext?: AppContext  ) => MessageReturn`|`-`||
|error|显示错误提示|`(    config: string \| MessageConfig,    appContext?: AppContext  ) => MessageReturn`|`-`||
|loading|显示加载中提示|`(    config: string \| MessageConfig,    appContext?: AppContext  ) => MessageReturn`|`-`||
|normal|显示提示|`(    config: string \| MessageConfig,    appContext?: AppContext  ) => MessageReturn`|`-`|2.41.0|
|clear|清空全部提示|`(position?: MessagePosition) => void`|`-`||



### MessageConfig

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|content|内容|`RenderContent`|`-`||
|id|唯一id|`string`|`-`||
|icon|消息的图标|`RenderFunction`|`-`||
|position|消息的位置|`'top'\|'bottom'`|`-`||
|showIcon|是否显示图标|`boolean`|`false`||
|closable|是否显示关闭按钮|`boolean`|`false`||
|duration|消息显示的持续时间|`number`|`-`||
|onClose|关闭时的回调函数|`(id: number \| string) => void`|`-`||
|resetOnHover|设置鼠标移入后不会自动关闭|`boolean`|`false`|2.39.0|



### MessageReturn

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|close|关闭当前消息|`() => void`|`-`|
