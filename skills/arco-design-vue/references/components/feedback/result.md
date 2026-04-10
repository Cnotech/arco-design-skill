---
name: arco-vue-result
description: "Arco Design Vue 结果页 Result 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-result>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 结果页 Result

来源组件：上游 `web-vue/components/result`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-result>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
展示结果状态。




```vue
<template>
  <a-result title="This is title content" subtitle="This is subtitle content">
    <template #extra>
      <a-space>
        <a-button type="secondary">Again</a-button>
        <a-button type="primary">Back</a-button>
      </a-space>
    </template>
  </a-result>
</template>
```

## 示例：成功状态

### 说明
展示成功状态。




```vue
<template>
  <a-result status="success" title="This is title content" >
    <template #subtitle>
      This is subtitle content
    </template>
    <template #extra>
      <a-space>
        <a-button type='primary'>Back</a-button>
      </a-space>
    </template>
  </a-result>
</template>
```

## 示例：警告状态

### 说明
展示警告状态。




```vue
<template>
  <a-result status="warning" title="This is title content">
    <template #subtitle>
      This is subtitle content
    </template>

    <template #extra>
      <a-space>
        <a-button type='primary'>Back</a-button>
      </a-space>
    </template>
  </a-result>
</template>
```

## 示例：错误状态

### 说明
展示错误状态。




```vue
<template>
  <a-result status="error" title="This is title content">
    <template #subtitle>
      This is subtitle content
    </template>

    <template #extra>
      <a-space>
        <a-button type='primary'>Back</a-button>
      </a-space>
    </template>
  </a-result>
</template>
```

## 示例：HTTP状态码 403

### 说明
没有当前页面的访问权限。




```vue
<template>
  <a-result
    status="403"
    subtitle="Access to this resource on the server is denied."
  >
    <template #extra>
      <a-space>
        <a-button type="primary">Back</a-button>
      </a-space>
    </template>
  </a-result>
</template>
```

## 示例：HTTP状态码 404

### 说明
页面未找到




```vue
<template>
  <a-result status="404" subtitle="Whoops, that page is gone.">
    <template #extra>
      <a-space>
        <a-button type="primary">Back</a-button>
      </a-space>
    </template>
  </a-result>
</template>
```

## 示例：HTTP状态码 500

### 说明
通常表示服务器错误




```vue
<template>
  <a-result status="500" subtitle="This page isn’t working.">
    <template #extra>
      <a-space>
        <a-button type="primary">Back</a-button>
      </a-space>
    </template>
  </a-result>
</template>
```

## 示例：自定义状态

### 说明
自定义状态。需要传入指定的图标




```vue
<template>
  <a-result :status="null" title="This is title content" subtitle="This is subtitle content">
    <template #icon>
      <IconFaceSmileFill />
    </template>
    <template #extra>
      <a-space>
        <a-button type="secondary">Again</a-button>
        <a-button type="primary">Back</a-button>
      </a-space>
    </template>
  </a-result>
</template>
<script>
import { IconFaceSmileFill } from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconFaceSmileFill
  },
}
</script>
```


## 示例：完整功能

### 说明
完整功能




```vue
<template>
  <a-result status="error" title="No internet ">
    <template #icon>
      <IconFaceFrownFill />
    </template>
    <template #subtitle> DNS_PROBE_FINISHED_NO_INTERNET </template>

    <template #extra>
      <a-button type="primary">Refresh</a-button>
    </template>
    <a-typography style="background: var(--color-fill-2); padding: 24px;">
      <a-typography-paragraph>Try:</a-typography-paragraph>
      <ul>
        <li> Checking the network cables, modem, and router </li>
        <li> Reconnecting to Wi-Fi </li>
      </ul>
    </a-typography>
  </a-result>
</template>

<script>
import { IconFaceFrownFill } from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconFaceFrownFill
  },
}
</script>
```

## API


### `<result>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|status|结果页显示的状态|`'info' \| 'success' \| 'warning' \| 'error' \| '403' \| '404' \| '500' \| null`|`'info'`|
|title|标题内容|`string`|`-`|
|subtitle|子标题内容|`string`|`-`|
### `<result>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|icon|图标|-||
|title|标题|-||
|subtitle|副标题|-||
|extra|操作区|-|2.8.0|
|default|默认插槽|-|2.8.0|
