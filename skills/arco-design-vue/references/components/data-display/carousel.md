---
name: arco-vue-carousel
description: "Arco Design Vue 图片轮播 Carousel 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-carousel>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 图片轮播 Carousel

来源组件：上游 `web-vue/components/carousel`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-carousel>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
基本用法




```vue
<template>
  <a-carousel
    :style="{
      width: '600px',
      height: '240px',
    }"
    :default-current="2"
    @change="handleChange"
  >
    <a-carousel-item v-for="image in images">
      <img
        :src="image"
        :style="{
          width: '100%',
        }"
      />
    </a-carousel-item>
  </a-carousel>
</template>

<script>
export default {
  setup() {
    const images = [
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/cd7a1aaea8e1c5e3d26fe2591e561798.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/6480dbc69be1b5de95010289787d64f1.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/0265a04fddbd77a19602a15d9d55d797.png~tplv-uwbnlip3yd-webp.webp',
    ];
    const handleChange=(value)=>{
      console.log(value)
    }
    return {
      images,
      handleChange
    }
  },
};
</script>
```

## 示例：自动切换

### 说明
可以通过 `autoPlay` 设置是否自动切换。
可设置 `moveSpeed`, `timingFunc` 实现不同切换幻灯片效果。




```vue
<template>
  <a-carousel
    :style="{
      width: '600px',
      height: '240px',
    }"
    :auto-play="true"
    indicator-type="dot"
    show-arrow="hover"
  >
    <a-carousel-item v-for="image in images">
      <img
        :src="image"
        :style="{
          width: '100%',
        }"
      />
    </a-carousel-item>
  </a-carousel>
</template>

<script>
export default {
  setup() {
    const images = [
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/cd7a1aaea8e1c5e3d26fe2591e561798.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/6480dbc69be1b5de95010289787d64f1.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/0265a04fddbd77a19602a15d9d55d797.png~tplv-uwbnlip3yd-webp.webp',
    ];
    return {
      images
    }
  },
};
</script>
```

## 示例：指示器

### 说明
可以指定指示器类型：`dot` | `line` | `slider` 和位置 `left` | `right` | `top` | `bottom` | `outer`。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-radio-group
      type="button"
      @change="updateType"
      style="{ marginBottom: '10px' }"
      :modelValue="indicatorType"
    >
      <a-radio value="dot">dot</a-radio>
      <a-radio value="line">line</a-radio>
      <a-radio value="slider">slider</a-radio>
    </a-radio-group>
    <a-radio-group
      type="button"
      @change="updatePosition"
      :style="{ marginBottom: '20px' }"
      :modelValue="indicatorPosition"
    >
      <a-radio value="left">left</a-radio>
      <a-radio value="right">right</a-radio>
      <a-radio value="top">top</a-radio>
      <a-radio value="bottom">bottom</a-radio>
      <a-radio value="outer">outer</a-radio>
    </a-radio-group>
    <a-carousel
      :indicator-type="indicatorType"
      :indicator-position="indicatorPosition"
      show-arrow="never"
      :style="{
      width: '600px',
      height: '240px',
    }"
    >
      <a-carousel-item v-for="image in images">
        <img
          :src="image"
          :style="{
          width: '100%',
        }"
        />
      </a-carousel-item>
    </a-carousel>
  </a-space>
</template>

<script>
export default {
  data() {
    return {
      images: [
        'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/cd7a1aaea8e1c5e3d26fe2591e561798.png~tplv-uwbnlip3yd-webp.webp',
        'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/6480dbc69be1b5de95010289787d64f1.png~tplv-uwbnlip3yd-webp.webp',
        'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/0265a04fddbd77a19602a15d9d55d797.png~tplv-uwbnlip3yd-webp.webp',
      ],
      indicatorType: 'dot',
      indicatorPosition: 'bottom',
    };
  },
  methods: {
    updateType(type) {
      this.indicatorType = type;
    },
    updatePosition(position) {
      this.indicatorPosition = position;
    },
  },
};
</script>
```

## 示例：切换方向

### 说明
默认情况下，`direction` 为 `horizontal`。通过设置 `direction` 为 `vertical` 来使用垂直方向切换。




```vue
<template>
  <a-carousel
    :style="{
      width: '600px',
      height: '240px',
    }"
    show-arrow="never"
    direction="vertical"
    indicator-position="right"
  >
    <a-carousel-item v-for="image in images">
      <img
        :src="image"
        :style="{
          width: '100%',
        }"
      />
    </a-carousel-item>
  </a-carousel>
</template>

<script>
export default {
  setup() {
    const images = [
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/cd7a1aaea8e1c5e3d26fe2591e561798.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/6480dbc69be1b5de95010289787d64f1.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/0265a04fddbd77a19602a15d9d55d797.png~tplv-uwbnlip3yd-webp.webp',
    ];
    return {
      images
    }
  },
};
</script>
```

## 示例：卡片化

### 说明
当页面宽度方向空间空余，但高度方向空间多余时，可指定 `animation` 为 `card` 使用卡片化风格。




```vue
<template>
  <a-carousel
    :autoPlay="true"
    animation-name="card"
    show-arrow="never"
    indicator-position="outer"
    :style="{
      width: '100%',
      height: '240px',
    }"
  >
    <a-carousel-item v-for="image in images" :style="{ width: '60%' }">
      <img
        :src="image"
        :style="{
          width: '100%',
        }"
      />
    </a-carousel-item>
  </a-carousel>
</template>

<script>
export default {
  setup() {
    const images = [
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/cd7a1aaea8e1c5e3d26fe2591e561798.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/6480dbc69be1b5de95010289787d64f1.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/0265a04fddbd77a19602a15d9d55d797.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/24e0dd27418d2291b65db1b21aa62254.png~tplv-uwbnlip3yd-webp.webp',
    ];
    return {
      images
    }
  },
};
</script>
```

## 示例：渐隐切换

### 说明
指定 `animation` 为 `fade` 使用渐隐切换效果。




```vue
<template>
  <a-carousel
    :style="{
      width: '600px',
      height: '240px',
    }"
    :auto-play="true"
    animation-name="fade"
    show-arrow="never"
  >
    <a-carousel-item v-for="image in images">
      <img
        :src="image"
        :style="{
          width: '100%',
        }"
      />
    </a-carousel-item>
  </a-carousel>
</template>

<script>
export default {
  setup() {
    const images = [
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/cd7a1aaea8e1c5e3d26fe2591e561798.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/6480dbc69be1b5de95010289787d64f1.png~tplv-uwbnlip3yd-webp.webp',
      'https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/0265a04fddbd77a19602a15d9d55d797.png~tplv-uwbnlip3yd-webp.webp',
    ];
    return {
      images
    }
  },
};
</script>
```

## API


### `<carousel>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|current **(v-model)**|当前展示索引|`number`|`-`|
|default-current|当前展示索引|`number`|`1`|
|auto-play|是否自动循环展示，或者传入 `{ interval: 自动切换的时间间隔(默认: 3000), hoverToPause: 鼠标悬浮时是否暂停自动切换(默认: true) }` 进行高级配置|`boolean \| CarouselAutoPlayConfig`|`false`|
|move-speed|幻灯片移动速率(ms)|`number`|`500`|
|animation-name|切换动画|`'slide' \| 'fade' \| 'card'`|`'slide'`|
|trigger|幻灯片切换触发方式, click/hover 指示器|`'click' \| 'hover'`|`'click'`|
|direction|幻灯片移动方向|`'horizontal' \| 'vertical'`|`'horizontal'`|
|show-arrow|切换箭头显示时机|`'always' \| 'hover' \| 'never'`|`'always'`|
|arrow-class|切换箭头样式|`string`|`''`|
|indicator-type|指示器类型，可为小方块和小圆点或不显示|`'line' \| 'dot' \| 'slider' \| 'never'`|`'dot'`|
|indicator-position|指示器位置|`'bottom' \| 'top' \| 'left' \| 'right' \| 'outer'`|`'bottom'`|
|indicator-class|指示器的样式|`string`|`''`|
|transition-timing-function|过渡速度曲线, 默认匀速 [transition-timing-function](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-timing-function)|`string`|`'cubic-bezier(0.34, 0.69, 0.1, 1)'`|
### `<carousel>` 事件

|事件名|描述|参数|
|---|---|---|
|change|幻灯片发生切换时的回调函数|index: `number`<br>prevIndex: `number`<br>isManual: `boolean`|
