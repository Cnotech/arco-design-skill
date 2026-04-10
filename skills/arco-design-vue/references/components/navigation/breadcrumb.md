---
name: arco-vue-breadcrumb
description: "Arco Design Vue 面包屑 Breadcrumb 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-breadcrumb>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 面包屑 Breadcrumb

来源组件：上游 `web-vue/components/breadcrumb`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-breadcrumb>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
面包屑的基本用法。




```vue
<template>
  <a-breadcrumb>
    <a-breadcrumb-item>Home</a-breadcrumb-item>
    <a-breadcrumb-item>Channel</a-breadcrumb-item>
    <a-breadcrumb-item>News</a-breadcrumb-item>
  </a-breadcrumb>
</template>
```

## 示例：自定义分隔符

### 说明
通过 `separator` 属性或插槽自定义分隔符。面包屑子项也可通过 `separator` 属性或插槽自定义分隔符，且优先级高于父项。




```vue
<template>
  <a-space direction="vertical">
    <a-breadcrumb>
      <template #separator>
        <icon-right />
      </template>
      <a-breadcrumb-item>Home</a-breadcrumb-item>
      <a-breadcrumb-item>Channel</a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
    <a-breadcrumb separator="~">
      <a-breadcrumb-item>Home</a-breadcrumb-item>
      <a-breadcrumb-item>Channel</a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
    <a-breadcrumb>
      <template #separator>
        <icon-right />
      </template>
      <a-breadcrumb-item separator="->">Home</a-breadcrumb-item>
      <a-breadcrumb-item>Channel</a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
  </a-space>
</template>
```

## 示例：自定义尺寸

### 说明
通过指定样式来自定义面包屑的尺寸。




```vue
<template>
  <a-space direction="vertical">
    <a-breadcrumb>
      <a-breadcrumb-item>Home</a-breadcrumb-item>
      <a-breadcrumb-item>Channel</a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
    <a-breadcrumb :style="{fontSize: `12px`}">
      <a-breadcrumb-item>Home</a-breadcrumb-item>
      <a-breadcrumb-item>Channel</a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
  </a-space>
</template>
```

## 示例：自定义图标

### 说明
可以在内容中使用自定义图标。




```vue
<template>
  <a-space direction="vertical">
    <a-breadcrumb>
      <a-breadcrumb-item>
        <icon-home/>
      </a-breadcrumb-item>
      <a-breadcrumb-item>Channel</a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
     <a-breadcrumb>
      <a-breadcrumb-item>
        <icon-home/>
      </a-breadcrumb-item>
      <a-breadcrumb-item>
        <icon-at />
        Channel
      </a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
  </a-space>
</template>
```

## 示例：参数化配置

### 说明
通过 `routes` 来传递面包屑数据。若是要自定义面包屑的话，建议使用 `<a-breadcrumb-item />` 组件。默认使用 `a` 标签的 `href` 属性绑定路径，可通过 `item` 插槽自定义渲染。




```vue
<template>
  <a-space direction="vertical">
    <a-breadcrumb :routes="routes"/>
    <a-breadcrumb :routes="routes">
      <template #item-render="{route, paths}">
        <a-link :href="paths.join('/')">
          {{route.label}}
        </a-link>
      </template>
    </a-breadcrumb>
  </a-space>
</template>

<script>
export default {
  data() {
    return {
      routes: [
        {
          path: '/',
          label: 'Home'
        },
        {
          path: '/channel',
          label: 'Channel',
        },
        {
          path: '/news',
          label: 'News'
        },
      ],
    }
  }
}
</script>
```

## 示例：带有下拉菜单

### 说明
通过 `droplist` 或者 `routes` 来指定下拉菜单。




```vue
<template>
  <a-space direction="vertical">
    <a-breadcrumb :routes="routes"/>
    <a-breadcrumb>
      <a-breadcrumb-item>Home</a-breadcrumb-item>
      <a-breadcrumb-item :droplist="droplist">
        Channel
      </a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
    <a-breadcrumb>
      <a-breadcrumb-item>Home</a-breadcrumb-item>
      <a-breadcrumb-item>
        <template #droplist>
          <a-doption>Option 1</a-doption>
          <a-dsubmenu value="option-1">
            <template #default>Option 2</template>
            <template #content>
              <a-doption>Option 2-1</a-doption>
              <a-doption>Option 2-2</a-doption>
              <a-doption>Option 2-3</a-doption>
            </template>
            <template #footer>
              <div style="padding: 6px; text-align: center;">
                <a-button>Click</a-button>
              </div>
            </template>
          </a-dsubmenu>
          <a-doption>Option 3</a-doption>
        </template>
        Channel
      </a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
    </a-breadcrumb>
  </a-space>
</template>

<script>
export default {
  data() {
    return {
      routes: [
        {
          path: '/',
          label: 'Home'
        },
        {
          path: '/channel',
          label: 'Channel',
          children: [
            {
              path: '/users',
              label: 'Users',
            },
            {
              path: '/permission',
              label: 'Permission',
            }
          ]
        },
        {
          path: '/news',
          label: 'News'
        },
      ],
      droplist: [
        {
          path: '/goods',
          label: 'Goods',
        },
        {
          path: '/wallet',
          label: 'Wallet',
        }
      ]
    }
  }
}
</script>
```

## 示例：显示省略

### 说明
通过 `max-count` 来指定面包屑的最多渲染数量，超出的部分将显示为省略号。




```vue
<template>
  <a-space direction="vertical">
    <a-breadcrumb :max-count="3">
      <a-breadcrumb-item>Home</a-breadcrumb-item>
      <a-breadcrumb-item>Sub Home</a-breadcrumb-item>
      <a-breadcrumb-item>All Channel</a-breadcrumb-item>
      <a-breadcrumb-item>Channel</a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
      <a-breadcrumb-item>Post</a-breadcrumb-item>
    </a-breadcrumb>
    <a-breadcrumb :max-count="3">
      <template #more-icon>
        <a-tooltip content="more routes a/b/c">
          <icon-more />
        </a-tooltip>
      </template>
      <a-breadcrumb-item>Home</a-breadcrumb-item>
      <a-breadcrumb-item>Sub Home</a-breadcrumb-item>
      <a-breadcrumb-item>All Channel</a-breadcrumb-item>
      <a-breadcrumb-item>Channel</a-breadcrumb-item>
      <a-breadcrumb-item>News</a-breadcrumb-item>
      <a-breadcrumb-item>Post</a-breadcrumb-item>
    </a-breadcrumb>
  </a-space>
</template>
```

## API


### `<breadcrumb>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|max-count|最多展示的面包屑数量（0表示不限制）|`number`|`0`||
|routes|设置路径|`BreadcrumbRoute[]`|`-`|2.36.0|
|separator|分隔符文字|`string\|number`|`-`|2.36.0|
|custom-url|自定义链接地址|`(paths: string[]) => string`|`-`|2.36.0|
### `<breadcrumb>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|more-icon|自定义更多图标|-|2.36.0|
|item-render|routes 设置时生效，自定义渲染面包屑|route: `BreadcrumbRoute`<br>routes: `BreadcrumbRoute[]`<br>paths: `string[]`|2.36.0|
|separator|自定义分隔符|-||




### `<breadcrumb-item>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|separator|分隔符文字|`string\|number`|`-`|2.36.0|
|droplist|下拉菜单内容|`BreadcrumbRoute['children']`|`-`|2.36.0|
|dropdown-props|下拉菜单属性|`DropDownProps`|`-`|2.36.0|
### `<breadcrumb-item>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|droplist|自定义下拉菜单|-|2.36.0|
|separator|自定义分隔符|-|2.36.0|




### BreadcrumbRoute

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|label|面包屑名称|`string`|`-`|
|path|跳转路径 (`a`标签的`href`)|`string`|`-`|
|children|下拉菜单展示项|`{    label: string;    path: string;  }[]`|`-`|



## Tips

同名的自定义插槽优先级是高于属性的
