---
name: arco-vue-notification
description: "Arco Design Vue 通知提醒框 Notification 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-notification>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 通知提醒框 Notification

来源组件：上游 `web-vue/components/notification`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 使用全局 Notification 服务：`this.$notification`、`getCurrentInstance().appContext.config.globalProperties.$notification`，或从 `@arco-design/web-vue` 导入 `Notification`。该 API 不是 `<a-notification>` 组件标签。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
通知提醒框的基本用法。




```vue
<template>
  <a-space>
    <a-button type="primary" @click="() => this.$notification.info({
      title:'Notification',
      content:'This is a notification!'
    })"
    >
      Open Notification
    </a-button>
    <a-button @click="handleNotification">
      Open Notification
    </a-button>
  </a-space>
</template>

<script>
import { Notification } from '@arco-design/web-vue';

export default {
  setup() {
    const handleNotification = () => {
      Notification.info({
        title: 'Notification',
        content: 'This is a notification!',
      })
    }

    return { handleNotification }
  }
}
</script>
```

## 示例：消息类型

### 说明
通知提醒框的消息类型。




```vue
<template>
  <a-space>
    <a-button
      type='primary'
      @click="() => this.$notification.info('This is an info message!')"
    >
      Info
    </a-button>
    <a-button
      type='primary'
      status="success"
      @click="() => this.$notification.success('This is a success message!')"
    >
      Success
    </a-button>
    <a-button
      type='primary'
      status="warning"
      @click="() => this.$notification.warning('This is a warning message!')"
    >
      Warning
    </a-button>
    <a-button
      type='primary'
      status="danger"
      @click="() => this.$notification.error('This is an error message!')"
    >
      Error
    </a-button>
    <a-button
      type='secondary'
      @click="() => this.$notification.info({
        content: 'This is an error message!',
        showIcon: false
      })"
    >
      Normal
    </a-button>
  </a-space>
</template>
```

## 示例：全局提示的位置

### 说明
通知提醒框有 4 种不同的弹出位置，分别为：`左上角`, `右上角 (默认)`, `左下角`, `右下角`。




```vue
<template>
  <a-space>
    <a-button type="primary" @click="handleNotification"> Top Right </a-button>
    <a-button type="primary" @click="handleNotificationTopLeft"> Top Left </a-button>
    <a-button type="primary" @click="handleNotificationBottomRight"> Bottom Right </a-button>
    <a-button type="primary" @click="handleNotificationBottomLeft"> Bottom Left </a-button>
  </a-space>
</template>

<script>
import { Notification } from '@arco-design/web-vue';

export default {
  setup() {
    const handleNotification = () => {
      Notification.info({
        title: 'Title',
        content: 'This is a Notification!',
      })
    }

    const handleNotificationTopLeft = () => {
      Notification.info({
        title: 'Title',
        content: 'This is a Notification!',
        position: "topLeft"
      })
    }

    const handleNotificationBottomRight = () => {
      Notification.info({
        title: 'Title',
        content: 'This is a Notification!',
        position: 'bottomRight'
      })
    }

    const handleNotificationBottomLeft = () => {
      Notification.info({
        title: 'Title',
        content: 'This is a Notification!',
        position: "bottomLeft"
      })
    }

    return {
      handleNotification,
      handleNotificationTopLeft,
      handleNotificationBottomRight,
      handleNotificationBottomLeft
    }
  }
}
</script>
```

## 示例：更新通知内容

### 说明
通过指定参数 `id`，可以更新已经存在的通知提醒框。




```vue
<template>
  <a-button type="primary" @click="handleNotification">
    Open Notification
  </a-button>
</template>

<script>
import { Notification } from '@arco-design/web-vue';

export default {
  setup() {
    const handleNotification = () => {
      Notification.warning({
        id: 'your_id',
        title: 'Ready to update',
        content: 'Will update after 2 seconds...',
      })

      setTimeout(() => {
        Notification.success({
          id: 'your_id',
          title: 'Success',
          content: 'Update success!',
        });
      }, 2000)
    }

    return { handleNotification }
  }
}
</script>
```

## 示例：更新延迟

### 说明
通过指定参数 `id`，可以更新已经存在的通知提醒框。




```vue
<template>
  <a-button type="primary" @click="handleNotification">
    Open Notification
  </a-button>
</template>

<script>
import { Notification } from '@arco-design/web-vue';

export default {
  setup() {
    const handleNotification = () => {
      Notification.warning({
        id: 'your_id',
        title: 'Ready to update',
        content: 'Will update after 2 seconds...',
        duration: 0,
      })

      setTimeout(() => {
        Notification.success({
          id: 'your_id',
          title: 'Success',
          content: 'Update success!',
          duration: 3000,
        });
      }, 2000)
    }

    return { handleNotification }
  }
}
</script>
```

## 示例：自定义操作按钮

### 说明
通过指定 `btn` 字段，可以添加操作按钮。




```vue
<template>
  <a-button type="primary" @click="handleNotification">
    Open Notification
  </a-button>
</template>

<script lang="jsx">
import { Notification, Space, Button } from '@arco-design/web-vue';

export default {
  setup() {
    const handleNotification = () => {
      const id = `${Date.now()}`;
      const closeNotification =  Notification.info({
        id,
        title:'Notification',
        content:'This is a notification!',
        duration: 0,
        footer: <Space>
          <Button
            type="secondary"
            size="small"
            onClick={() => Notification.remove(id)}
          >
            Cancel
          </Button>
          <Button type="primary" size="small" onClick={closeNotification}>
            Ok
          </Button>
        </Space>
      })
    }

    return { handleNotification }
  }
}
</script>
```

## 示例：自定义关闭按钮

### 说明
需要设置 `closable: true`，自定义元素使用 `closeIconElement`，仅图标使用 `closeIcon` (会有 `hover` 样式)。




```vue
<template>
  <a-space>
    <a-button type="primary" @click="handleNotification">
      Open Notification
    </a-button>
    <a-button type="primary" status="danger" @click="handleNotification2">
      Open Notification
    </a-button>
  </a-space>
</template>

<script lang="jsx">
import { Notification, Button } from '@arco-design/web-vue';
import { IconCloseCircle } from '@arco-design/web-vue/es/icon';

export default {
  setup() {
    const handleNotification = () => {
      Notification.info({
        title:'Notification',
        content:'This is a notification!',
        closable: true,
        closeIcon: <IconCloseCircle />
      })
    }

    const handleNotification2 = () => {
      Notification.error({
        title:'Notification',
        content:'This is a notification!',
        closable: true,
        closeIconElement: <Button size="mini">Close</Button>
      })
    }

    return { handleNotification, handleNotification2 }
  }
}
</script>
```

## 示例：自定义样式

### 说明
可以设置 `style` 和 `class` 来定制样式。




```vue
<template>
  <a-button type="primary" @click="handleNotification">
    Open Notification
  </a-button>
</template>

<script>
import { Notification } from '@arco-design/web-vue';

export default {
  setup() {
    const handleNotification = () => {
      Notification.info({
        title: 'Notification',
        content: 'This is a notification!',
        closable: true,
        style: { width: '500px' }
      })
    }

    return { handleNotification }
  }
}
</script>
```

## API





### `Notification` 全局方法

`Notification` 提供的全局方法，可以通过以下三种方法使用：
1. 通过 `this.$notification` 调用
2. 在 Composition API 中，通过 `getCurrentInstance().appContext.config.globalProperties.$notification` 调用
3. 导入 `Notification`，通过 `Notification` 本身调用

当通过 `import` 方式使用时，组件没有办法获取当前的 Vue Context，如 i18n 或 route 等注入在 AppContext 上的内容无法在内部使用，需要在调用时手动传入 AppContext，或者为组件全局指定 AppContext

```ts
import { createApp } from 'vue'
import { Notification } from '@arco-design/web-vue';

const app = createApp(App);
Notification._context = app._context;
```


### NotificationMethod

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|info|显示信息提醒框|`(    config: string \| NotificationConfig,    appContext?: AppContext  ) => NotificationReturn`|`-`|
|success|显示成功提醒框|`(    config: string \| NotificationConfig,    appContext?: AppContext  ) => NotificationReturn`|`-`|
|warning|显示警告提醒框|`(    config: string \| NotificationConfig,    appContext?: AppContext  ) => NotificationReturn`|`-`|
|error|显示错误提醒框|`(    config: string \| NotificationConfig,    appContext?: AppContext  ) => NotificationReturn`|`-`|
|remove|清除对应 `id` 的提醒框|`(id: string) => void`|`-`|
|clear|清除全部提醒框|`(position?: NotificationPosition) => void`|`-`|



### NotificationConfig

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|content|内容|`RenderContent`|`-`||
|title|标题|`RenderContent`|`-`||
|icon|图标|`RenderFunction`|`-`||
|id|唯一id|`string`|`-`||
|style|样式|`CSSProperties`|`-`||
|class|样式类名|`ClassName`|`-`||
|position|位置|`'topLeft'\|'topRight'\|'bottomLeft'\|'bottomRight'`|`-`||
|showIcon|是否显示图标|`boolean`|`true`||
|closable|是否可关闭|`boolean`|`false`||
|duration|显示的持续时间，单位为 `ms`|`number`|`3000`||
|footer|底部内容|`RenderFunction`|`-`|2.25.0|
|closeIcon|关闭按钮图标|`RenderFunction`|`-`||
|closeIconElement|关闭按钮元素|`RenderFunction`|`-`||
|onClose|关闭时的回调函数|`(id: number \| string) => void`|`-`||



### NotificationReturn

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|close|关闭当前通知提醒框|`() => void`|`-`|
