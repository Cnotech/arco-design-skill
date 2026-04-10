---
name: arco-vue-auto-complete
description: "Arco Design Vue 自动补全 AutoComplete 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-auto-complete>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 自动补全 AutoComplete

来源组件：上游 `web-vue/components/auto-complete`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-auto-complete>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
自动补全的基础用法




```vue
<template>
  <a-auto-complete :data="data" @search="handleSearch" :style="{width:'360px'}" placeholder="please enter something"/>
</template>

<script>
export default {
  data() {
    return {
      data: []
    }
  },
  methods: {
    handleSearch(value) {
      if (value) {
        this.data = [...Array(5)].map((_, index) => `${value}-${index}`)
        console.log(this.data)
      } else {
        this.data = []
      }
    }
  }
}
</script>
```

## 示例：区分大小写

### 说明
使用 `strict` 属性来指明在匹配时严格区分大小写。




```vue

<template>
  <a-auto-complete :data="data" :style="{width:'360px'}" placeholder="please enter something" strict />
</template>

<script>
export default {
  data() {
    return {
      data: ['Beijing', 'Shanghai', 'Chengdu', 'WuHan']
    }
  },
}
</script>
```

## 示例：弹出框的页脚

### 说明
自定义弹出框的页脚




```vue
<template>
  <a-auto-complete :data="data" @search="handleSearch" :style="{width:'360px'}" placeholder="please enter something">
    <template #footer>
      <div style="padding: 6px 0; text-align: center;">
        <a-button>Click Me</a-button>
      </div>
    </template>
  </a-auto-complete>
</template>

<script>
export default {
  data() {
    return {
      data: []
    }
  },
  methods: {
    handleSearch(value) {
      if (value) {
        this.data = [...Array(5)].map((_, index) => `${value}-${index}`)
        console.log(this.data)
      } else {
        this.data = []
      }
    }
  }
}
</script>
```

## API


### `<auto-complete>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`string`|`-`||
|default-value|默认值（非受控模式）|`string`|`''`||
|disabled|是否禁用|`boolean`|`false`||
|data|用于自动提示的数据|`(string \| number \| SelectOptionData \| SelectOptionGroup)[]`|`[]`||
|popup-container|弹出框的挂载容器|`string \| HTMLElement \| null \| undefined`|`-`||
|strict|是否为严格校验模式|`boolean`|`false`||
|filter-option|自定义选项过滤方法|`FilterOption`|`true`||
|trigger-props|trigger 组件属性|`TriggerProps`|`-`|2.14.0|
|allow-clear|是否允许清空输入框|`boolean`|`false`|2.23.0|
|virtual-list-props|传递虚拟列表属性，传入此参数以开启虚拟滚动 [VirtualListProps](#VirtualListProps)|`VirtualListProps`|`-`|2.50.0|
### `<auto-complete>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|change|绑定值发生改变时触发|value: `string`||
|search|用户搜索时触发|value: `string`||
|select|选择选项时触发|value: `string`||
|clear|用户点击清除按钮时触发|ev: `Event`|2.23.0|
|dropdown-scroll|下拉菜单发生滚动时触发|ev: `Event`|2.52.0|
|dropdown-reach-bottom|下拉菜单滚动到底部时触发|ev: `Event`|2.52.0|
### `<auto-complete>` 方法

|方法名|描述|参数|返回值|版本|
|---|---|---|---|:---|
|focus|使输入框获取焦点|-|-|2.40.0|
|blur|使输入框失去焦点|-|-|2.40.0|
### `<auto-complete>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|option|选项内容|data: `OptionInfo`|2.13.0|
|footer|弹出框的页脚|-||
