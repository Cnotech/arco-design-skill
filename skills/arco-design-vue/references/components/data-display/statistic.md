---
name: arco-vue-statistic
description: "Arco Design Vue 数值显示 Statistic 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-statistic>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 数值显示 Statistic

来源组件：上游 `web-vue/components/statistic`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-statistic>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
当需要突出某个或某组数字或展示带描述的统计类数据时使用。




```vue
<template>
  <a-space size="large">
    <a-statistic title="Downloads" :value="125670" show-group-separator />
    <a-statistic extra="Comments" :value="40509" :precision="2" />
  </a-space>
</template>
```

## 示例：自定义前缀&后缀

### 说明
通过 `prefix` 和 `suffix` 插槽可以添加前后缀。




```vue
<template>
  <a-space size="large">
    <a-statistic title="New Users" :value="125670" show-group-separator >
      <template #suffix>
        <icon-arrow-rise />
      </template>
    </a-statistic>
    <a-statistic title="User Growth Rate" :value="50.52" :precision="2" :value-style="{ color: '#0fbf60' }">
      <template #prefix>
        <icon-arrow-rise />
      </template>
      <template #suffix>%</template>
    </a-statistic>
  </a-space>
</template>
```

## 示例：数值动画

### 说明
通过 `animation` 可以开启数值动画。




```vue
<template>
  <a-statistic title="User Growth Rate" :value="50.52" :precision="2" :value-from="0" :start="start" animation>
    <template #prefix>
      <icon-arrow-rise />
    </template>
    <template #suffix>%</template>
  </a-statistic>
  <a-button @click="start=true">Start</a-button>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const start = ref(false);

    return {
      start
    }
  },
}
</script>
```

## 示例：倒计时组件

### 说明
倒计时组件 `countdown` 的基本使用方法。




```vue
<template>
  <a-row>
    <a-col :flex="1">
      <a-countdown
        title="Countdown"
        :value="now + 1000 * 60 * 60 * 2"
        :now="now"
      />
    </a-col>
    <a-col :flex="1">
      <a-countdown
        title="Milliseconds"
        :value="now + 1000 * 60 * 60 * 2"
        :now="now"
        format="HH:mm:ss.SSS"
      />
    </a-col>
    <a-col :flex="1">
      <a-countdown
        title="Days"
        :value="now + 1000 * 60 * 60 * 24 * 4"
        :now="now"
        format="D 天 H 时 m 分 s 秒"
      />
    </a-col>
  </a-row>
  <a-space direction="vertical" style="margin-top: 10px">
    <a-countdown
      title="Trigger on finish"
      :value="Date.now() + 5 * 1000"
      format="mm:ss.SSS"
      :now="Date.now()"
      :start="start"
      @finish="handleFinish"
    />
    <a-button @click="start = true" type="primary">Start</a-button>
  </a-space>
</template>

<script>
import { ref } from 'vue';
import { Message } from '@arco-design/web-vue';

export default {
  setup() {
    const now = Date.now();
    const start = ref(false);

    const handleFinish = () => {
      Message.info('Finish');
    };

    return {
      now,
      start,
      handleFinish,
    };
  },
};
</script>
```

## API


### `<statistic>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|title|数值显示的标题|`string`|`-`||
|value|数值显示的值|`number \| Date`|`-`||
|format|数值显示的格式 [dayjs](https://day.js.org/docs/en/display/format)（日期模式使用）|`string`|`'HH:mm:ss'`||
|extra|额外的显示内容|`string`|`-`||
|start|是否开始动画|`boolean`|`true`||
|precision|小数保留位数（数字模式使用）|`number`|`0`||
|separator|进位分隔符（数字模式使用）|`string`|`-`||
|show-group-separator|是否展示进位分隔符（数字模式使用）|`boolean`|`false`||
|animation|是否开启动画|`boolean`|`false`||
|animation-duration|动画的过度时间|`number`|`2000`||
|value-from|动画的起始值|`number`|`-`||
|placeholder|提示文字（当 value 为 undefined 时显示）|`string`|`-`|2.28.0|
|value-style|自定义显示值的样式|`CSSProperties`|`-`|2.32.0|
### `<statistic>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|title|标题|-|
|prefix|前缀|-|
|suffix|后缀|-|
|extra|额外内容|-|




### `<countdown>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|title|倒计时的标题|`string`|`-`||
|value|倒计时的值|`number`|`() => Date.now() + 300000`||
|now|用于修正初始化时间显示不正确|`number`|`() => Date.now()`||
|format|倒计时的展示格式 [dayjs](https://day.js.org/docs/en/display/format)|`string`|`'HH:mm:ss'`||
|start|是否开始倒计时|`boolean`|`true`||
|value-style|自定义显示值的样式|`CSSProperties`|`-`|2.32.0|
### `<countdown>` 事件

|事件名|描述|参数|
|---|---|---|
|finish|倒计时完成后触发的回调|-|
### `<countdown>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|title|标题|-|
