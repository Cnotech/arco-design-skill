---
name: arco-vue-progress
description: "Arco Design Vue 进度条 Progress 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-progress>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 进度条 Progress

来源组件：上游 `web-vue/components/progress`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-progress>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
简单的进度条。




```vue
<template>
  <a-progress :percent="0.2" :style="{width:'50%'}" />
  <br/>
  <br/>
  <a-progress :percent="0.3" :style="{width:'50%'}">
    <template v-slot:text="scope" >
      进度 {{scope.percent * 100}}%
    </template>
  </a-progress>
</template>
```

## 示例：进度条状态

### 说明
通过 `status` 指定进度条状态




```vue
<template>
  <a-space direction="vertical" :style="{width: '50%'}">
    <a-progress :percent="percent" />
    <a-progress status='warning' :percent="percent" />
    <a-progress status='danger' :percent="percent" />
  </a-space>
  <div :style="{marginTop:'20px'}">
    <a-slider v-model="percent" :max="1" :step="0.1" :style="{width: '150px'}" />
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const percent = ref(0.2);

    return {
      percent
    }
  },
}
</script>
```

## 示例：环形进度条

### 说明
设置 `type="circle"` 将会展示环形进度条。




```vue

<template>
  <a-space size="large">
    <a-progress type="circle" :percent="percent" />
    <a-progress type="circle" status='warning' :percent="percent" />
    <a-progress type="circle" status='danger' :percent="percent" />
    <a-progress type="circle" status='success' :percent="percent" />
  </a-space>
  <div :style="{marginTop:'20px'}">
    <a-slider v-model="percent" :max="1" :step="0.1" :style="{width: '150px'}" />
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const percent = ref(0.2);

    return {
      percent
    }
  },
}
</script>
```

## 示例：迷你进度条

### 说明
设置 `size="mini"` 展示微型进度条。




```vue
<template>
  <a-space size="large" :style="{width: '100%'}">
    <a-progress size="mini" :percent="percent"/>
    <a-progress size="mini" status='warning' :percent="percent"/>
    <a-progress size="mini" status='danger' :percent="percent"/>
    <a-progress size="mini" status='success' :percent="percent"/>
  </a-space>
  <a-space size="large" :style="{width: '100%', marginTop: '20px'}">
    <a-progress type="circle" size="mini" :percent="percent"/>
    <a-progress type="circle" size="mini" status='warning' :percent="percent"/>
    <a-progress type="circle" size="mini" status='danger' :percent="percent"/>
    <a-progress type="circle" size="mini" status='success' :percent="percent"/>
  </a-space>
  <div :style="{marginTop: '20px'}">
    <a-slider v-model="percent" :max="1" :step="0.1" :style="{width: '150px'}" />
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const percent = ref(0.2);

    return {
      percent
    }
  },
}
</script>
```

## 示例：进度条大小

### 说明
通过 `size` 设置进度条的大小




```vue
<template>
  <a-space direction="vertical" size="large" :style="{width:'50%'}">
    <a-radio-group v-model="size" type="button">
      <a-radio value="small">Small</a-radio>
      <a-radio value="medium">Medium</a-radio>
      <a-radio value="large">Large</a-radio>
    </a-radio-group>
    <a-progress :size="size" :percent="0.2"/>
    <a-progress status='warning' :size="size" :percent="0.2"/>
    <a-progress status='danger' :size="size" :percent="0.2"/>
    <a-space>
      <a-progress type="circle" :size="size" :percent="0.2"/>
      <a-progress type="circle" status='warning' :size="size" :percent="0.2"/>
      <a-progress type="circle" status='danger' :size="size" :percent="0.2"/>
    </a-space>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    return {
      size: ref('medium')
    }
  }
}
</script>
```

## 示例：渐变进度条

### 说明
`color` 传入对象时， 会作为 `linear-gradient` 的属性值设置渐变色。




```vue
<template>
  <div>
    <a-progress
      :percent="0.8"
      :style="{ width: '50%' }"
      :color="{
        '0%': 'rgb(var(--primary-6))',
        '100%': 'rgb(var(--success-6))',
      }"
    />
    <br/>
    <br/>

    <a-progress
      :percent="1"
      :style="{ width: '50%' }"
      :color="{
        '0%': 'rgb(var(--primary-6))',
        '100%': 'rgb(var(--success-6))',
      }"
    />
    <br/>
    <br/>
    <a-space size="large">
      <a-progress
        type="circle"
        :percent="0.8"
        :style="{ width: '50%' }"
        :color="{
          '0%': 'rgb(var(--primary-6))',
          '100%': 'rgb(var(--success-6))',
        }"
      />

      <a-progress
        type="circle"
        :percent="1"
        :style="{ width: '50%' }"
        :color="{
          '0%': 'rgb(var(--primary-6))',
          '100%': 'rgb(var(--success-6))',
        }"
      />
    </a-space>
  </div>
</template>
```

## 示例：步骤进度条

### 说明
通过设置 `steps` 展示步骤进度条。




```vue
<template>
  <div :style="{ width: '50%' }">
    <a-progress :steps="3" :percent="0.3" />
    <a-progress :steps="5" status="warning" :percent="1" />
    <a-progress :steps="3" size="small" :percent="0.3" />
  </div>
</template>
```

## 示例：剩余进度条的颜色

### 说明
可以通过 trackColor 设置剩余进度条的颜色




```vue
<template>
  <div :style="{ width: '50%' }">
    <a-progress
      :percent="0.4"
      trackColor="var(--color-primary-light-1)"
      style="margin-bottom: 20px;"
    />
    <a-progress
      :percent="0.4"
      :steps="4"
      trackColor="var(--color-primary-light-1)"
      style="margin-bottom: 20px;"
    />
    <a-progress
      :percent="0.4"
      type="circle"
      trackColor="var(--color-primary-light-1)"
      style="margin-bottom: 20px;"
    />
  </div>
</template>
```

## API


### `<progress>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|进度条的类型|`'line' \| 'circle'`|`'line'`|
|size|进度条的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`|
|percent|进度条当前的百分比|`number`|`0`|
|steps|开启步骤条模式，并设置步骤数|`number`|`0`|
|animation|是否开启过渡动画|`boolean`|`false`|
|stroke-width|进度条的线宽|`number`|`-`|
|width|进度条的长度|`number\|string`|`-`|
|color|进度条的颜色|`string\|object`|`-`|
|track-color|进度条的轨道颜色|`string`|`-`|
|show-text|是否显示文字|`boolean`|`true`|
|status|进度条状态|`'normal' \| 'success' \| 'warning' \| 'danger'`|`-`|
