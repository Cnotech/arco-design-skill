---
name: arco-vue-badge
description: "Arco Design Vue 徽标数 Badge 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-badge>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 徽标数 Badge

来源组件：上游 `web-vue/components/badge`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-badge>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
基本用法。只需指定 `count`或者 `content slot`，即可显示徽标。




```vue
<template>
  <a-space :size="40">
    <a-badge :count="9">
      <a-avatar shape="square" />
    </a-badge>
    <a-badge :count="9" dot :dotStyle="{ width: '10px', height: '10px' }">
      <a-avatar shape="square" />
    </a-badge>
    <a-badge :dotStyle="{ height: '16px', width: '16px', fontSize: '14px' }">
      <template #content>
        <IconClockCircle
          :style="{ verticalAlign: 'middle', color: 'var(--color-text-2)' }"
        />
      </template>
      <a-avatar shape="square" />
    </a-badge>
  </a-space>
</template>

<script>
import { IconClockCircle } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconClockCircle },
};
</script>
```

## 示例：独立使用

### 说明
`default slot` 为空时，将会独立展示徽标。




```vue
<template>
  <a-space :size="40">
    <a-badge :count="2" />
    <a-badge
      :count="2"
      :dotStyle="{ background: '#E5E6EB', color: '#86909C' }"
    />
    <a-badge :count="16" />
    <a-badge :count="1000" :max-count="99" />
  </a-space>
</template>
```

## 示例：小红点

### 说明
设置 `dot`，即可只显示小红点而不显示数字。`count > 0` 时才显示。




```vue
<template>
  <a-space :size="40">
    <a-badge :count="9" dot :offset="[6, -2]">
      <a href="#">Link</a>
    </a-badge>
    <a-badge :count="9" dot :offset="[2, -2]">
      <IconNotification
        :style="{ color: '#888', fontSize: '18px', verticalAlign: '-3px' }"
      />
    </a-badge>
  </a-space>
</template>

<script>
import { IconNotification } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconNotification },
};
</script>
```

## 示例：文本内容

### 说明
设置 `text`，可设置自定义提示内容。




```vue
<template>
  <a-space :size="40">
    <a-badge text="NEW">
      <a-avatar shape="square">
        <span>
          <IconUser />
        </span>
      </a-avatar>
    </a-badge>
    <a-badge text="HOT">
      <a-avatar shape="square">
        <span>
          <IconUser />
        </span>
      </a-avatar>
    </a-badge>
  </a-space>
</template>

<script>
import { IconUser } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconUser },
};
</script>
```

## 示例：最大值

### 说明
设置 `max-count`，可以限制最大显示的徽标数值，超过将会加 `+` 后缀。`max-count` 默认为 `99`。




```vue
<template>
  <a-space :size="40">
    <a-badge :max-count="10" :count="0">
      <a-avatar shape="square">
        <span>
          <IconUser />
        </span>
      </a-avatar>
    </a-badge>
    <a-badge :max-count="10" :count="100">
      <a-avatar shape="square">
        <span>
          <IconUser />
        </span>
      </a-avatar>
    </a-badge>
    <a-badge :count="100">
      <a-avatar shape="square">
        <span>
          <IconUser />
        </span>
      </a-avatar>
    </a-badge>
    <a-badge :max-count="999" :count="1000">
      <a-avatar shape="square">
        <span>
          <IconUser />
        </span>
      </a-avatar>
    </a-badge>
  </a-space>
</template>

<script>
import { IconUser } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconUser },
};
</script>
```

## 示例：状态点

### 说明
设置 `status`，可以得到不同的状态点。`normal - 正常` `processing - 进行中` `success - 成功` `warning - 提醒` `danger - 危险`。




```vue
<template>
  <a-space size="large" direction="vertical">
    <a-space size="large">
      <a-badge status="normal" />
      <a-badge status="processing" />
      <a-badge status="success" />
      <a-badge status="warning" />
      <a-badge status="danger" />
    </a-space>
    <a-space size="large">
      <a-badge status="normal" text="Normal" />
      <a-badge status="processing" text="Processing" />
      <a-badge status="success" text="Success" />
      <a-badge status="warning" text="Warning" />
      <a-badge status="danger" text="Danger" />
    </a-space>
  </a-space>
</template>
```

## 示例：颜色

### 说明
我们提供多种预设色彩的徽标样式。如果预设值不能满足你的需求，`color` 字段也可以设置自定义色值。




```vue
<template>
  <div>
    <a-badge
      v-for="color in colors"
      :key="color"
      :color="color"
      :text="color"
      :style="{ marginRight: '24px' }"
    />
  </div>
  <br />
  <div>
    <a-badge
      v-for="color in customColors"
      :key="color"
      :color="color"
      :text="color"
      :style="{ marginRight: '24px' }"
    />
  </div>
</template>

<script>
const COLORS = [
  'red',
  'orangered',
  'orange',
  'gold',
  'lime',
  'green',
  'cyan',
  'arcoblue',
  'purple',
  'pinkpurple',
  'magenta',
  'gray',
];

const COLORS_CUSTOM = [
  '#F53F3F',
  '#7816FF',
  '#00B42A',
  '#165DFF',
  '#FF7D00',
  '#EB0AA4',
  '#7BC616',
  '#86909C',
  '#B71DE8',
  '#0FC6C2',
  '#FFB400',
  '#168CFF',
  '#FF5722',
];
export default {
  data() {
    return {
      colors: COLORS,
      customColors: COLORS_CUSTOM,
    };
  },
};
</script>
```

## API


### `<badge>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|text|自定义提示内容|`string`|`-`|
|dot|显示为小红点|`boolean`|`false`|
|dot-style|徽标的样式|`object`|`-`|
|max-count|徽标最大显示数值，如果count超过这个数值会显示为maxCount|`number`|`99`|
|offset|设置徽标位置的偏移|`number[]`|`[]`|
|color|内置的一些颜色|`ColorType \| string`|`-`|
|status|徽标的状态类型|`'normal' \| 'processing' \| 'success' \| 'warning' \| 'danger'`|`-`|
|count|徽标显示的数字|`number`|`-`|
