---
name: arco-vue-image
description: "Arco Design Vue 图片 Image 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-image>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 图片 Image

来源组件：上游 `web-vue/components/image`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-image>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
需要查看图片的时候，简单的设置 `src` 属性，就能获得一个有预览图片功能的组件。




```vue
<template>
  <a-image
    width="200"
    src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp"
  />
</template>
```

## 示例：显示 Caption

### 说明
通过设置 `title` 和 `description` 可以将图片的标题和描述显示在图片内部或者底部，显示的位置通过 `footerPosition` 控制。




```vue
<template>
  <a-image
    width="200px"
    :src="src"
    :title="title"
    :description="description"
  />
  <a-image
    width="200px"
    :src="src"
    :title="title"
    :description="description"
    footerPosition="outer"
    style="margin-left: 67px; vertical-align: top;"
  />
</template>

<script>
export default {
  setup() {
    return {
      src: 'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp',
      title: 'A user’s avatar',
      description: 'Present by Arco Design',
    }
  }
}
</script>
```

## 示例：额外操作

### 说明
组件提供了具名插槽 `extra` 供用户在页脚定制额外的内容。




```vue
<template>
  <a-image
    src='https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp'
    title='A user’s avatar'
    description='Present by Arco Design'
    width="260"
    style="margin-right: 67px; vertical-align: top;"
    :preview-visible="visible1"
    @preview-visible-change="() => { visible1= false }"
  >
    <template #extra>
      <div class="actions">
        <span class="action" @click="() => { visible1 = true }"><icon-eye /></span>
        <span class="action" @click="onDownLoad"><icon-download /></span>
        <a-tooltip content="A user’s avatar">
          <span class="action"><icon-info-circle /></span>
        </a-tooltip>
      </div>
    </template>
  </a-image>
  <a-image
    src='https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp'
    title='A user’s avatar'
    description='Present by Arco Design'
    width="260"
    footer-position="outer"
    :preview-visible="visible2"
    @preview-visible-change="() => { visible2 = false }"
  >
    <template #extra>
      <div class="actions actions-outer">
        <span class="action" @click="() => { visible2 = true }"><icon-eye /></span>
        <span class="action" @click="onDownLoad"><icon-download /></span>
        <a-tooltip content="A user’s avatar">
          <span class="action"><icon-info-circle /></span>
        </a-tooltip>
      </div>
    </template>
  </a-image>
</template>
<script>
  import { ref } from 'vue';
  import { IconEye, IconDownload, IconInfoCircle } from '@arco-design/web-vue/es/icon';

  export default {
    components: {
      IconEye, IconDownload, IconInfoCircle
    },
    setup() {
      const visible1 = ref(false);
      const visible2 = ref(false);

      return {
        visible1,
        visible2,
        onDownLoad() {
          console.log('download');
        },
      }
    }
  }
</script>
<style scoped>
  .actions {
    display: flex;
    align-items: center;
  }
  .action {
    padding: 5px 4px;
    font-size: 14px;
    margin-left: 12px;
    border-radius: 2px;
    line-height: 1;
    cursor: pointer;
  }
  .action:first-child {
    margin-left: 0;
  }

  .action:hover {
    background: rgba(0,0,0,.5);
  }
  .actions-outer {
    .action {
      &:hover {
        color: #ffffff;
      }
    }
  }
</style>
```

## 示例：错误状态

### 说明
当加载图片失败的时候显示的内容。




```vue
<template>
  <a-space :size="20">
    <a-image
      width="400"
      height="300"
      src="some-error.png"
    />
    <a-image
      width="400"
      height="300"
      src="some-error.png"
      alt="This is a picture of humans eating ice cream. The humans on the screen are very happy just now. The ice cream is green, it seems to be flavored with matcha. The gender of the human is unknown. It has very long hair and the human hair is brown."
    />
  </a-space>
</template>
```

## 示例：加载状态

### 说明
默认情况下，加载效果是不显示的，可通过设置 `showLoader` 为 `true` 显示默认加载效果。如果默认加载效果不符合需求, 还可以通过 具名插槽 `loader` 自行设置加载样式。




```vue
<template>
  <div>
    <a-button
      type="primary"
      @click="() => {timestamp = Date.now()}"
      style="margin-bottom: 20px;"
    >
      reload
    </a-button>
  </div>
  <a-image
    width="200"
    height="200"
    :src="`https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp?timestamp=${timestamp}`"
    show-loader
  />
  <a-image
    width="200"
    height="200"
    :src="`https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp?timestamp=${timestamp}`"
    style="marginLeft: 67px"
  >
    <template #loader>
      <div class="loader-animate"/>
    </template>
  </a-image>
</template>
<script>
  import { ref } from 'vue';
  export default {
    setup() {
      const timestamp = ref('');
      return {
        timestamp,
      }
    }
  }
</script>
<style scoped>
  .loader-animate {
    width: 100%;
    height: 100%;
    background: linear-gradient(
      -60deg,
      var(--color-fill-2) 25%,
      var(--color-neutral-3) 40%,
      var(--color-fill-3) 55%
    );
    background-size: 400% 100%;
    animation: loop-circle 1.5s cubic-bezier(0.34, 0.69, 0.1, 1) infinite;
  }

  @keyframes loop-circle {
    0% {
      background-position: 100% 50%;
    }

    100% {
      background-position: 0 50%;
    }
  }
</style>
```

## 示例：渐进加载

### 说明
大图可通过给 `loader` 传递一个小一些的图片，让其在原图未被加载成功时显示，以此来模拟渐进加载。




```vue
<template>
  <div>
    <a-button
      type="primary"
      @click="() => {timestamp = Date.now()}"
      style="margin-bottom: 20px;"
    >
      reload
    </a-button>
  </div>
  <a-image
    width="200"
    height="200"
    :src="`https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp?timestamp=${timestamp}`"
  >
    <template #loader>
      <img
        width="200"
        src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp"
        style="filter: blur(5px);"
      />
    </template>
  </a-image>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const timestamp = ref('');
    return {
      timestamp,
    }
  }
}
</script>
```

## 示例：自定义预览操作栏

### 说明
通过设置 `actionsLayout` 可以调整预览操作栏中功能按钮的顺序，同时可以过滤功能按钮，只有在 `actionsLayout` 中的按钮才会出现。
此外从 `2.17.0` 开始，预览组件 `a-image-preview` 提供了 `actions` 插槽，支持自定义额外的操作项，同时还提供了操作项组件 `a-image-preview-action`。




```vue
<template>
  <a-image
    width="200"
    src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp"
    :preview-props="{
      actionsLayout: ['rotateRight', 'zoomIn', 'zoomOut'],
    }"
  >
    <template #preview-actions>
      <a-image-preview-action name="下载" @click="download"><icon-download /></a-image-preview-action>
    </template>
  </a-image>
</template>

<script>
export default {
  setup() {
    const download = () => {
      console.log('点击下载图片')
    };

    return {
      download
    }
  },
}
</script>
```

## 示例：多图预览

### 说明
用 `<a-image-preview-group>` 包裹 `<a-image>` 组件即可进行多图预览。




```vue
<template>
  <a-image-preview-group infinite>
    <a-space>
      <a-image src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/cd7a1aaea8e1c5e3d26fe2591e561798.png~tplv-uwbnlip3yd-webp.webp" width="200" />
      <a-image src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/6480dbc69be1b5de95010289787d64f1.png~tplv-uwbnlip3yd-webp.webp" width="200" />
      <a-image src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/0265a04fddbd77a19602a15d9d55d797.png~tplv-uwbnlip3yd-webp.webp" width="200" />
      <a-image src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/24e0dd27418d2291b65db1b21aa62254.png~tplv-uwbnlip3yd-webp.webp" width="200" />
    </a-space>
  </a-image-preview-group>
</template>
```

## 示例：单独使用预览组件

### 说明
`a-image-preview` 可单独使用，需要手动控制 `visible`。




```vue
<template>
  <a-button type="primary" @click="onClick">Click me to preview image</a-button>
  <a-image-preview
    src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp"
    v-model:visible="visible"
  />
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visible = ref(false)
    const onClick = () => {
      visible.value = true;
    };

    return {
      visible,
      onClick,
    };
  },
};
</script>
```

## 示例：单独使用多图预览组件

### 说明
`<a-image-preview-group>` 可单独使用，需控制 `visible` 。在图片的展示上分为两种场景，一是通过 `defaultCurrent` 指定第一张展示的图片；二是控制 `current` 来决定当前显示的是第几张图片。




```vue
<template>
  <a-button type="primary" @click="onClick">Click me to preview multiple image</a-button>
  <a-image-preview-group
    v-model:visible="visible"
    v-model:current="current"
    infinite
    :srcList="[
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/cd7a1aaea8e1c5e3d26fe2591e561798.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/6480dbc69be1b5de95010289787d64f1.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/0265a04fddbd77a19602a15d9d55d797.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/24e0dd27418d2291b65db1b21aa62254.png~tplv-uwbnlip3yd-webp.webp',
    ]"
  />
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const visible = ref(false)
    const current = ref(3);
    const onClick = () => {
      visible.value = true;
    };

    return {
      visible,
      current,
      onClick,
    };
  },
}
</script>
```

## 示例：挂载节点

### 说明
可以通过 `popupContainer` 指定预览挂载的父级节点。




```vue
<template>
  <div
    id="image-demo-preview-popup-container"
    :style="{
      width: '100%',
      height: '400px',
      backgroundColor: 'var(--color-fill-2)',
      position: 'relative',
      overflow: 'hidden',
      lineHeight: '400px',
      textAlign: 'center',
    }"
  >
    <a-image
      width="200"
      src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp"
      :preview-props="{
        popupContainer: '#image-demo-preview-popup-container',
        closable: false,
      }"
    />
  </div>
</template>
```

## API


### `<image>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|src|图片获取地址|`string`|`-`||
|width|图片显示宽度|`string \| number`|`-`||
|height|图片显示高度|`string \| number`|`-`||
|title|标题|`string`|`-`||
|description|描述，将显示在底部，如果 alt 没有值，则会将其设置给 alt|`string`|`-`||
|fit|确定图片如何适应容器框|`'contain' \| 'cover' \| 'fill' \| 'none' \| 'scale-down'`|`-`||
|alt|图片的文字描述|`string`|`-`||
|hide-footer|是否隐藏 footer（2.36.0 版本支持 'never' 参数，支持在加载错误时显示底部内容）|`boolean \| 'never'`|`false`||
|footer-position|底部显示的位置|`'inner' \| 'outer'`|`'inner'`||
|show-loader|是否显示加载中效果|`boolean`|`false`||
|preview|是否开启预览|`boolean`|`true`||
|preview-visible **(v-model)**|控制预览的打开状态，可与 previewVisibleChange 配合使用|`boolean`|`-`||
|default-preview-visible|预览的默认打开状态|`boolean`|`false`||
|preview-props|预览的配置项（所有选项都是可选的） [ImagePreviewProps](#image-preview%20Props)|`ImagePreviewProps`|`-`||
|footer-class|底部显示区域的类名|`string\|array\|object`|`-`|2.23.0|
### `<image>` 事件

|事件名|描述|参数|
|---|---|---|
|preview-visible-change|预览的打开和关闭事件|visible: `boolean`|
### `<image>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|error|自定义错误状态内容|-|
|error-icon|自定义错误状态的图标|-|
|loader|自定义加载状态效果|-|
|extra|底部额外内容|-|




### `<image-preview>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|src|图片获取地址|`string`|`-`|
|visible **(v-model)**|是否可见|`boolean`|`-`|
|default-visible|默认是否可见，非受控|`boolean`|`false`|
|mask-closable|点击 mask 是否触发关闭|`boolean`|`true`|
|closable|是否显示关闭按钮|`boolean`|`true`|
|actions-layout|操作项的布局|`string[]`|`[  'fullScreen',  'rotateRight',  'rotateLeft',  'zoomIn',  'zoomOut',  'originalSize',]`|
|popup-container|设置弹出框的挂载点，同 `teleport` 的 `to`，缺省值是 document.body|`HTMLElement \| string`|`-`|
|esc-to-close|是否支持 ESC 键关闭预览|`boolean`|`true`|
|wheel-zoom|是否开启滚轮缩放|`boolean`|`true`|
|keyboard|是否开启键盘控制|`boolean`|`true`|
|default-scale|默认缩放比|`number`|`1`|
|zoom-rate|缩放速率，仅对滚动缩放生效|`number`|`1.1`|
### `<image-preview>` 事件

|事件名|描述|参数|
|---|---|---|
|close|关闭事件|-|
### `<image-preview>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|actions|自定义额外的操作项|-|2.17.0|




### `<image-preview-group>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|src-list|图片列表（设置了本属性之后，将不再收集 a-image 子组件的图片信息）|`string[]`|`-`|
|current **(v-model)**|当前展示的图片的下标|`number`|`-`|
|default-current|第一张展示的图片的下标|`number`|`0`|
|infinite|是否无限循环|`boolean`|`false`|
|visible **(v-model)**|是否可见，受控属性|`boolean`|`-`|
|default-visible|默认是否可见，非受控|`boolean`|`false`|
|mask-closable|点击 mask 是否触发关闭|`boolean`|`true`|
|closable|是否显示关闭按钮|`boolean`|`true`|
|actions-layout|控制条的布局|`string[]`|`[  'fullScreen',  'rotateRight',  'rotateLeft',  'zoomIn',  'zoomOut',  'originalSize',]`|
|popup-container|设置弹出框的挂载点，同 `teleport` 的 `to`，缺省值是 document.body|`string \| HTMLElement`|`-`|
### `<image-preview-group>` 事件

|事件名|描述|参数|
|---|---|---|
|change|切换图片|index: `number`|
|visible-change|预览的打开和关闭|visible: `boolean`|
### `<image-preview-group>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|actions|自定义额外的操作项|-|2.46.0|




### `<image-preview-action>` 属性 (2.17.0)

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|name|名称|`string`|`-`|
|disabled|是否禁用|`boolean`|`false`|



## FAQ

### 关于 `image-preview` 的属性说明

1. 键盘快捷键 `keyboard` 设置此属性为 `true` 后，将根据 `actions-layout` 操作项来启用相应的快捷键操作。
- `esc`: 关闭预览
- `left`: 切换至上一张图片
- `right`: 切换至下一张图片
- `up`: 放大图片
- `down`: 缩小图片
- `space`: 还原至原始大小

2. 默认缩放比例 `defaultScale` 此属性定义了默认的图片缩放比例。例如，当设置为 1.5 时，图片将默认放大到原始大小的 1.5 倍。

3. 滚动缩放速率 `zoomSate` 属性控制了在滚动操作时图片的缩放速率。以 1.3 为例，每次滚动操作都会使图片放大或缩小 1.3 倍。
