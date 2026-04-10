---
name: arco-vue-trigger
description: "Arco Design Vue 触发器 Trigger 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-trigger>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 触发器 Trigger

来源组件：上游 `web-vue/components/trigger`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-trigger>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
这个例子展示了触发器的最基础的使用。触发器默认是没有弹出框的样式的。以下示例均为官网添加的样式。



```vue
<template>
  <a-space>
    <a-trigger position="top" auto-fit-position :unmount-on-close="false">
      <span>Hover Me</span>
      <template #content>
        <div class="demo-basic">
          <a-empty />
        </div>
      </template>
    </a-trigger>
    <a-trigger trigger="click" :unmount-on-close="false">
      <a-button>Click Me</a-button>
      <template #content>
        <div class="demo-basic">
          <a-empty />
        </div>
      </template>
    </a-trigger>
    <a-trigger trigger="focus">
      <a-input placeholder="Focus on me" />
      <template #content>
        <div class="demo-basic">
          <a-empty />
        </div>
      </template>
    </a-trigger>
  </a-space>
</template>

<style scoped>
.demo-basic {
  padding: 10px;
  width: 200px;
  background-color: var(--color-bg-popup);
  border-radius: 4px;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, 0.15);
}
</style>
```

## 示例：多层嵌套

### 说明
弹出层可以嵌套在另一个弹出层内。



```vue
<template>
  <a-trigger trigger="click">
    <a-button>Click Me</a-button>
    <template #content>
      <div class="trigger-demo-nest">
        <a-empty />
        <a-trigger position="right">
          <a-button>Hover Me</a-button>
          <template #content>
            <div class="trigger-demo-nest">
              <a-empty />
              <a-trigger trigger="click" position="right">
                <a-button>Click Me</a-button>
                <template #content>
                  <div class="trigger-demo-nest">
                    <a-empty />
                    <a-trigger position="right">
                      <a-button>Hover Me</a-button>
                      <template #content>
                        <a-empty class="trigger-demo-nest" />
                      </template>
                    </a-trigger>
                  </div>
                </template>
              </a-trigger>
            </div>
          </template>
        </a-trigger>
      </div>
    </template>
  </a-trigger>
</template>

<style scoped>
.trigger-demo-nest {
  padding: 10px;
  width: 200px;
  background-color: var(--color-bg-popup);
  border-radius: 4px;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, 0.15);
}

.trigger-demo-nest-popup-content {
  text-align: right;
}
</style>
```

## 示例：多个触发方式

### 说明
通过`trigger`传入数组，可以设置多个触发方式。



```vue
<template>
  <a-trigger :trigger="['click','hover','focus']">
    <a-input placeholder="Click/Hover/Focus on me" />
    <template #content>
      <div class="demo-trigger">
        <a-empty />
      </div>
    </template>
  </a-trigger>
</template>

<style scoped>
.demo-trigger {
  padding: 10px;
  width: 200px;
  background-color: var(--color-bg-popup);
  border-radius: 4px;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, 0.15);
}
</style>
```

## 示例：跟随鼠标显示弹出框

### 说明
设置`align-point`属性，可以使弹出层出现在鼠标位置。



```vue
<template>
  <a-trigger trigger="click" align-point>
    <div class="demo-point-trigger">
      <div>Click Me</div>
    </div>
    <template #content>
      <div class="demo-point">
        <a-empty />
      </div>
    </template>
  </a-trigger>
</template>

<style scoped>
.demo-point-trigger {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 300px;
  background-color: var(--color-fill-2)
}

.demo-point {
  padding: 10px;
  width: 200px;
  background-color: var(--color-bg-popup);
  border-radius: 4px;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, 0.15);
}

.demo-point-wrapper {
  display: block;
}
</style>
```

## 示例：滚动容器

### 说明
通过设置 `update-at-scroll` 监听容器的滚动。




```vue
<template>
  <div :style="{height:'100px',overflowY:'scroll'}">
    <div :style="{height:'200px'}">
      <a-trigger trigger="click" update-at-scroll>
        <a-button :style="{marginTop:'80px'}">Click Me</a-button>
        <template #content>
          <div class="demo-basic">
            <a-empty />
          </div>
        </template>
      </a-trigger>
    </div>
  </div>
</template>

<style scoped>
.demo-basic {
  padding: 10px;
  width: 200px;
  background-color: var(--color-bg-popup);
  border-radius: 4px;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, 0.15);
}
</style>
```

## 示例：显示箭头元素

### 说明
通过`show-arrow`属性，可以展示默认的箭头元素。也可以通过`arrow-class`或`arrow-style`进行定制。



```vue
<template>
  <a-space>
    <a-trigger trigger="click">
      <a-button>Click Me</a-button>
      <template #content>
        <div class="demo-arrow">
          <a-empty />
        </div>
      </template>
    </a-trigger>
    <a-trigger trigger="click" show-arrow>
      <a-button>Click Me (Arrow)</a-button>
      <template #content>
        <div class="demo-arrow">
          <a-empty />
        </div>
      </template>
    </a-trigger>
  </a-space>
</template>

<style scoped>
.demo-arrow {
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, 0.15);
  padding: 10px;
  width: 200px;
  background-color: var(--color-bg-popup);
  border-radius: 4px;
}
</style>
```

## 示例：弹窗偏移量

### 说明
通过`popup-translate`属性，可以设置弹窗在原本位置的基础上进行额外的位置调整。



```vue
<template>
  <a-space>
    <a-trigger>
      <a-button>BOTTOM</a-button>
      <template #content>
        <div class="trigger-demo-translate">
          <a-empty />
        </div>
      </template>
    </a-trigger>
    <a-trigger :popup-translate="[100, 20]">
      <a-button>BOTTOM OFFSET[100, 20]</a-button>
      <template #content>
        <div class="trigger-demo-translate">
          <a-empty />
        </div>
      </template>
    </a-trigger>
    <a-trigger :popup-translate="[-100, 20]">
      <a-button>BOTTOM OFFSET[-100, 20]</a-button>
      <template #content>
        <div class="trigger-demo-translate">
          <a-empty />
        </div>
      </template>
    </a-trigger>
  </a-space>
</template>

<style scoped>
.trigger-demo-translate {
  padding: 10px;
  width: 200px;
  background-color: var(--color-bg-popup);
  border-radius: 4px;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, 0.15);
}
</style>
```

## API


### `<trigger>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|popup-visible **(v-model)**|弹出框是否可见|`boolean`|`-`||
|default-popup-visible|弹出框默认是否可见（非受控模式）|`boolean`|`false`||
|trigger|触发方式|`'hover' \| 'click' \| 'focus' \| 'contextMenu'`|`'hover'`||
|position|弹出位置|`'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'`|`'bottom'`||
|disabled|触发器是否禁用|`boolean`|`false`||
|popup-offset|弹出框的偏移量（弹出框距离触发器的偏移距离）|`number`|`0`||
|popup-translate|弹出框的移动距离|`TriggerPopupTranslate`|`-`||
|show-arrow|弹出框是否显示箭头|`boolean`|`false`||
|align-point|弹出框是否跟随鼠标|`boolean`|`false`||
|popup-hover-stay|是否在移出触发器，并移入弹出框时保持弹出框显示|`boolean`|`true`||
|blur-to-close|是否在触发器失去焦点时关闭弹出框|`boolean`|`true`||
|click-to-close|是否在点击触发器时关闭弹出框|`boolean`|`true`||
|click-outside-to-close|是否在点击外部区域时关闭弹出框|`boolean`|`true`||
|unmount-on-close|是否在关闭时卸载弹出框节点|`boolean`|`true`||
|content-class|弹出框内容的类名|`string\|array\|object`|`-`||
|content-style|弹出框内容的样式|`CSSProperties`|`-`||
|arrow-class|弹出框箭头的类名|`string\|array\|object`|`-`||
|arrow-style|弹出框箭头的样式|`CSSProperties`|`-`||
|popup-style|弹出框的样式|`CSSProperties`|`-`||
|animation-name|弹出动画的name|`string`|`'fade-in'`||
|duration|弹出动画的持续时间|`number\| {    enter: number;    leave: number;  }`|`-`||
|mouse-enter-delay|mouseenter事件延时触发的时间（毫秒）|`number`|`100`||
|mouse-leave-delay|mouseleave事件延时触发的时间（毫秒）|`number`|`100`||
|focus-delay|focus事件延时触发的时间（毫秒）|`number`|`0`||
|auto-fit-popup-width|是否将弹出框宽度设置为触发器宽度|`boolean`|`false`||
|auto-fit-popup-min-width|是否将弹出框的最小宽度设置为触发器宽度|`boolean`|`false`||
|auto-fix-position|当触发器的尺寸发生变化时，是否重新计算弹出框位置|`boolean`|`true`||
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`-`||
|update-at-scroll|是否在容器滚动时更新弹出框的位置|`boolean`|`false`||
|auto-fit-position|是否自动调整弹出框位置，以适应窗口大小|`boolean`|`true`||
|render-to-body|是否挂载在 `body` 元素下|`boolean`|`true`||
|prevent-focus|是否阻止弹出层中的元素点击时获取焦点|`boolean`|`false`||
|scroll-to-close|是否在滚动时关闭弹出框|`boolean`|`false`|2.46.0|
|scroll-to-close-distance|滚动阈值，当滚动距离超过该值时触发关闭|`number`|`0`||
### `<trigger>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|popup-visible-change|弹出框显示状态改变时触发|visible: `boolean`||
|show|弹出框显示后（动画结束）触发|-|2.18.0|
|hide|弹出框隐藏后（动画结束）触发|-|2.18.0|
### `<trigger>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|content|弹出框内容|-|



## Type

```ts
type TriggerPopupTranslate =
  | [number, number]
  | { [key in TriggerPosition]?: [number, number] };
```

## FAQ

### 关于弹出框的挂载位置

弹出框默认是挂载到 `body` 元素上的，如果想要修改挂载元素，可以使用 `popup-container` 属性进行指定，同时需要注意保证挂载元素的位置可以被准确定位到，一般可以为挂载元素增加 `position: relative` 样式。

在微前端项目中，需要保证子应用的挂载位置准确，可以将子应用的 `body` 样式添加 `position: relative`

### 滚动触发容器

组件默认仅监听了 `window` 的滚动事件，对于内部 `div` 的滚动没有进行监听，类似 `scroll-to-close` 功能也仅会对 `window` 滚动生效。可以通过开启 `update-at-scroll` 属性支持对父级 `div` 元素的滚动事件监听。
