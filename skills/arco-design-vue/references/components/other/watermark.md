---
name: arco-vue-watermark
description: "Arco Design Vue 水印 Watermark 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-watermark>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 水印 Watermark

来源组件：上游 `web-vue/components/watermark`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-watermark>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
水印的基本用法。




```vue
<template>
  <a-watermark content="arco.design">
    <div style="width: 100%; height: 350px;" />
  </a-watermark>
</template>
```

## 示例：多行文本

### 说明
通过 content 设置字符串数组可指定多行文字水印内容。




```vue
<template>
  <a-watermark :content="['arco.design',dayjs().format('YYYY-MM-DD')]">
    <div style="width: 100%; height: 300px;" />
  </a-watermark>
</template>
<script>
import dayjs from 'dayjs';

export default {
  setup() {
    return {
      dayjs,
    }
  }
}
</script>
```

## 示例：图片水印

### 说明
通过 image 设置图片水印。建议使用 2 倍或 3 倍图（支持Base64）。




```vue
<template>
  <a-watermark content="acro.design" grayscale image="">
    <div style="width: 100%; height: 300px;" />
  </a-watermark>
</template>
```

## 示例：自定义

### 说明
通过自定义参数以实现更多的水印效果。




```vue
<template>
  <a-form size="small" :model="form" auto-label-width>
    <a-row :gutter="16">
      <a-col :span="24">
        <a-form-item field="rotate" label="rotate">
          <a-slider v-model="form.rotate" :min="-180" :max="180" />
        </a-form-item>
      </a-col>
      <a-col :span="12">
        <a-form-item label="gap">
          <a-input-group>
            <a-input-number
              v-model="form.gap[0]"
              placeholder="gap[x]"
              :min="0"
            />
            <a-input-number
              v-model="form.gap[1]"
              placeholder="gap[y]"
              :min="0"
            />
          </a-input-group>
        </a-form-item>
      </a-col>
      <a-col :span="12">
        <a-form-item label="offset">
          <a-input-group>
            <a-input-number v-model="form.offset[0]" placeholder="offsetLeft" />
            <a-input-number v-model="form.offset[1]" placeholder="offsetTop" />
          </a-input-group>
        </a-form-item>
      </a-col>
      <a-col :span="12">
        <a-form-item label="fontSize">
          <a-input-number v-model="form.font.fontSize" mode="button" />
        </a-form-item>
      </a-col>
      <a-col :span="12">
        <a-form-item label="zIndex">
          <a-input-number v-model="form.zIndex" mode="button" />
        </a-form-item>
      </a-col>
      <a-col :span="6">
        <a-form-item label="repeat">
          <a-switch v-model="form.repeat" />
        </a-form-item>
      </a-col>
      <a-col :span="6">
        <a-form-item label="staggered">
          <a-switch v-model="form.staggered" />
        </a-form-item>
      </a-col>
    </a-row>
  </a-form>
  <a-watermark content="arco.design" v-bind="form">
    <div style="width: 100%; border: 1px solid #e5e6eb; box-sizing: border-box">
      <a-typography-title :heading="5"> Design system </a-typography-title>
      <a-typography>
        <a-typography-paragraph>
          A design is a plan or specification for the construction of an object
          or system or for the implementation of an activity or process, or the
          result of that plan or specification in the form of a prototype,
          product or process. The verb to design expresses the process of
          developing a design.
        </a-typography-paragraph>
        <a-typography-paragraph>
          A design is a plan or specification for the construction of an object
          or system or for the implementation of an activity or process, or the
          result of that plan or specification in the form of a prototype,
          product or process. The verb to design expresses the process of
          developing a design.
        </a-typography-paragraph>
      </a-typography>
      <img
        style="position: relative; z-index: 7"
        src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/24e0dd27418d2291b65db1b21aa62254.png~tplv-uwbnlip3yd-webp.webp"
      />
    </div>
  </a-watermark>
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      rotate: 0,
      gap: [50, 50],
      offset: [],
      font: { fontSize: 16 },
      zIndex: 6,
      repeat: true,
      staggered: true,
    });
    return {
      form,
    };
  },
};
</script>
```

## API


### `<watermark>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|content|水印文字内容|`string \| string[]`|`-`|
|image|图片源，建议使用 2 倍或 3 倍图|`string`|`-`|
|width|水印宽度（默认为内容宽度）|`number`|`-`|
|height|水印高度（默认为内容高度）|`number`|`-`|
|gap|水印间的间距|`[number, number]`|`() => [90, 90]`|
|offset|距离容器左上角的偏移量，默认为水印间距的一半|`[number, number]`|`[gap[0]/2, gap[1]/2]`|
|rotate|旋转角度|`number`|`-22`|
|font|水印字体样式，具体参数配置看 [WatermarkFont](#WatermarkFont)|`WatermarkFont`|`-`|
|z-index|水印层级|`number`|`6`|
|alpha|透明度|`number`|`1`|
|anti-tamper|水印防篡改|`boolean`|`true`|
|grayscale|灰阶水印|`boolean`|`false`|
|repeat|是否重复水印|`boolean`|`true`|
|staggered|是否错开排列|`boolean`|`true`|




### WatermarkFont

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|color|字体颜色|`string`|`rgba(0, 0, 0, 0.15)`|
|fontSize|字体大小|`number`|`16`|
|fontFamily|字体类型|`string`|`sans-serif`|
|fontStyle|字体样式|`'none' \| 'normal' \| 'italic' \| 'oblique'`|`normal`|
|textAlign|字体对齐方式|`'start' \| 'end' \| 'left' \| 'right' \| 'center'`|`center`|
|fontWeight|字体粗细|`'normal' \| 'bold' \| 'bolder' \| 'lighter' \| number`|`normal`|
