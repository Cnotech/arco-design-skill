---
name: arco-vue-icon
description: "Arco Design Vue Icon 图标参考。用于 `@arco-design/web-vue/es/icon`、`ArcoVueIcon`、`<icon-xx>`、图标按需导入、图标属性、旋转图标和 iconfont.cn 集成。"
user-invocable: false
---

# Icon 图标

来源文档：
- 上游 `packages/arco-vue-docs/pages/icon/__demo__/basic.md`
- 上游 `packages/arco-vue-docs/pages/icon/__demo__/spin.md`
- 上游 `packages/arco-vue-docs/pages/icon/__demo__/tree-shaking.md`
- 上游 `packages/arco-vue-docs/pages/icon/__demo__/icon-font.md`

Arco 图标通过独立图标入口提供。

## 全局注册

当应用需要使用大量 `<icon-xx>` 图标标签时，可以一次性注册图标库。

```ts
import { createApp } from 'vue';
import ArcoVue from '@arco-design/web-vue';
import ArcoVueIcon from '@arco-design/web-vue/es/icon';
import '@arco-design/web-vue/dist/arco.css';
import App from './App.vue';

const app = createApp(App);
app.use(ArcoVue);
app.use(ArcoVueIcon);
app.mount('#app');
```

注册后即可使用 `<icon-check-circle />` 这类标签。

```vue
<template>
  <a-space size="large">
    <icon-check-circle :style="{ fontSize: '32px' }" />
    <icon-check-circle :style="{ fontSize: '32px' }" :stroke-width="2" />
    <icon-check-circle :style="{ fontSize: '32px' }" stroke-linecap="round" />
    <icon-check-circle :style="{ fontSize: '32px' }" stroke-linejoin="arcs" />
  </a-space>
</template>
```

## 按需导入

只导入当前组件实际使用的图标。

```vue
<script setup lang="ts">
import { IconPlus, IconCheckCircle } from '@arco-design/web-vue/es/icon';
</script>

<template>
  <a-space size="large">
    <IconPlus :style="{ fontSize: '32px' }" />
    <IconCheckCircle :style="{ fontSize: '32px' }" />
  </a-space>
</template>
```

## 旋转图标

通过设置 `spin` 可以让图标处于旋转状态；也可以使用 `rotate` 自定义旋转角度。

```vue
<template>
  <a-space size="large">
    <icon-refresh :style="{ fontSize: '32px' }" spin />
    <icon-sync :style="{ fontSize: '32px' }" spin />
    <icon-face-smile-fill :style="{ fontSize: '32px' }" :rotate="180" />
  </a-space>
</template>
```

## 图标属性

| 属性 | 说明 | 类型 | 默认值 |
|---|---|---|---|
| `strokeWidth` | 线宽 | `number` | `4` |
| `strokeLinecap` | 端点类型 | `'butt' \| 'round' \| 'square'` | `'butt'` |
| `strokeLinejoin` | 拐角类型 | `'arcs' \| 'bevel' \| 'miter' \| 'miter-clip' \| 'round'` | `'miter'` |
| `rotate` | 旋转角度 | `number` | `-` |
| `spin` | 是否旋转 | `boolean` | `false` |
| `size` | 尺寸 | `number \| string` | `-` |

## iconfont.cn

使用 `Icon.addFromIconFontCn` 接入 iconfont.cn 的 symbol 项目。

```vue
<script setup lang="ts">
import { Icon } from '@arco-design/web-vue';

const IconFont = Icon.addFromIconFontCn({
  src: 'https://at.alicdn.com/t/font_180975_ue66sq60vyd.js',
});
</script>

<template>
  <a-space size="large">
    <IconFont type="icon-person" :size="32" />
    <IconFont type="icon-earth" :size="32" />
  </a-space>
</template>
```

`IconFontOptions`：

| 参数 | 说明 | 类型 | 默认值 |
|---|---|---|---|
| `src` | iconfont.cn 项目生成的在线 JS 地址 | `string` | `-` |
| `extraProps` | 传递给内部 Icon 组件的额外属性 | `object` | `-` |

iconfont.cn 集成暂不支持按需加载。
