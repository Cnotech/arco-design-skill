---
name: arco-vue-steps
description: "Arco Design Vue 步骤条 Steps 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-steps>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 步骤条 Steps

来源组件：上游 `web-vue/components/steps`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-steps>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
步骤条的基本用法。




```vue
<template>
  <div>
    <a-steps :current="2">
      <a-step>Succeeded</a-step>
      <a-step>Processing</a-step>
      <a-step>Pending</a-step>
    </a-steps>
    <a-divider/>
    <div style="line-height: 140px; text-align: center; color: #C9CDD4; ">
      Step 2 Content
    </div>
  </div>
</template>
```

## 示例：描述信息

### 说明
通过设置 `description` 可以添加描述信息。




```vue
<template>
  <a-steps>
    <a-step description="This is a description">Succeeded</a-step>
    <a-step description="This is a description">Processing</a-step>
    <a-step description="This is a description">Pending</a-step>
  </a-steps>
</template>
```

## 示例：标签放置位置

### 说明
通过设置 `label-placement` 可以改变标签描述文字放置的位置。放置位置分为 `horizontal` - **放置在图标右侧（默认）**、`vertical` - **放置在图标下方**两种。




```vue
<template>
  <a-steps label-placement="vertical">
    <a-step description="This is a description">Succeeded</a-step>
    <a-step description="This is a description">Processing</a-step>
    <a-step description="This is a description">Pending</a-step>
  </a-steps>
</template>
```

## 示例：步骤错误

### 说明
通过设置 `status="error"` 来展示错误状态。




```vue
<template>
  <a-steps :current="2" status="error">
    <a-step description="This is a description">Succeeded</a-step>
    <a-step description="This is a description">Error</a-step>
    <a-step description="This is a description">Pending</a-step>
  </a-steps>
</template>
```

## 示例：自定义图标

### 说明
通过 `#icon` 插槽可以自定义节点图标。





```vue
<template>
  <a-steps>
    <a-step description="This is a description">
      Succeeded
      <template #icon>
        <icon-home/>
      </template>
    </a-step>
    <a-step description="This is a description">
      Processing
      <template #icon>
        <icon-loading/>
      </template>
    </a-step>
    <a-step description="This is a description">
      Pending
      <template #icon>
        <icon-thumb-up/>
      </template>
    </a-step>
  </a-steps>
</template>
```

## 示例：隐藏连接线

### 说明
通过设置 `line-less` 可以使用无连接线模式。




```vue
<template>
  <a-steps :current="2" line-less>
    <a-step description="This is a description">Succeeded</a-step>
    <a-step description="This is a description">Processing</a-step>
    <a-step description="This is a description">Pending</a-step>
  </a-steps>
</template>
```

## 示例：竖直步骤条

### 说明
竖直方向的步骤条。




```vue
<template>
  <div class="frame-bg">
    <div class="frame-body">
      <div class="frame-aside">
        <a-steps :current="current" direction="vertical">
          <a-step>Succeeded</a-step>
          <a-step>Processing</a-step>
          <a-step>Pending</a-step>
        </a-steps>
      </div>
      <div class="frame-main">
        <div class="main-content">The content of this step.</div>
        <div class="main-bottom">
          <a-button :disabled="current===1" @click="onPrev">
            <icon-left />
            Back
          </a-button>
          <a-button :disabled="current===3" @click="onNext">
            Next
            <icon-right />
          </a-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const current = ref(1);

    const onPrev = () => {
      current.value = Math.max(1, current.value - 1);
    };

    const onNext = () => {
      current.value = Math.min(3, current.value + 1);
    };

    return {
      current,
      onPrev,
      onNext,
    }
  },
};
</script>

<style scoped lang="less">
.frame-bg {
  max-width: 780px;
  padding: 40px;
  background: var(--color-fill-2);
}

.frame-body {
  display: flex;
  background: var(--color-bg-2);
}

.frame-aside {
  padding: 24px;
  height: 272px;
  border-right: 1px solid var(--color-border);
}

.frame-main {
  width: 100%;
}

.main-content {
  text-align: center;
  line-height: 200px;
}

.main-bottom {
  display: flex;
  justify-content: center;

  button {
    margin: 0 20px;
  }
}
</style>
```

## 示例：箭头步骤条

### 说明
通过设置 `type="arrow"`，可以使用箭头类型的步骤条。**注意**：仅支持水平步骤条。




```vue
<template>
  <a-steps type="arrow" :current="2">
    <a-step description="This is a description">Succeeded</a-step>
    <a-step description="This is a description">Processing</a-step>
    <a-step description="This is a description">Pending</a-step>
  </a-steps>
</template>
```

## 示例：点状步骤条

### 说明
通过设置 `type="dot"` ， 可以使用点状的步骤条。此模式没有 small 尺寸。




```vue
<template>
  <a-steps type="dot">
    <a-step>Succeeded</a-step>
    <a-step>Processing</a-step>
    <a-step>Pending</a-step>
  </a-steps>
</template>
```

## 示例：导航步骤条

### 说明
通过设置 `type="navigation"` 展示导航类型的步骤条。




```vue
<template>
  <a-steps type="navigation">
    <a-step>Succeeded</a-step>
    <a-step>Processing</a-step>
    <a-step>Pending</a-step>
  </a-steps>
</template>
```

## 示例：可切换步骤条

### 说明
设置 `changeable` 开启点击切换步骤。




```vue
<template>
  <div>
    <a-steps changeable :current="current" @change="setCurrent">
      <a-step description="This is a description">Succeeded</a-step>
      <a-step description="This is a description">Processing</a-step>
      <a-step description="This is a description">Pending</a-step>
    </a-steps>
    <div :style="{
          width: '100%',
          height: '200px',
          textAlign: 'center',
          background: 'var(--color-bg-2)',
          color: '#C2C7CC',
        }">
      <div style="line-height: 160px;">Step{{current}} Content</div>
      <a-space size="large">
        <a-button type="secondary" :disabled="current <= 1" @click="onPrev">
          <IconLeft/> Back
        </a-button>
        <a-button type="primary" :disabled="current >= 3" @click="onNext">
          Next <IconRight/>
        </a-button>
      </a-space>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      current: 1,
    };
  },
  methods: {
    onPrev() {
      this.current = Math.max(1, this.current - 1)
    },

    onNext() {
      this.current = Math.min(3, this.current + 1)
    },

    setCurrent(current) {
      this.current = current
    }
  }
};
</script>
```

## API


### `<steps>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|步骤条的类型|`'default' \| 'arrow' \| 'dot' \| 'navigation'`|`'default'`|
|direction|步骤条的显示方向|`'horizontal' \| 'vertical'`|`'horizontal'`|
|label-placement|标签描述文字放置的位置|`'horizontal' \| 'vertical'`|`'horizontal'`|
|current **(v-model)**|当前步骤数|`number`|`-`|
|default-current|默认的步骤数（非受控状态）|`number`|`1`|
|status|当前步骤的状态|`'wait' \| 'process' \| 'finish' \| 'error'`|`'process'`|
|line-less|是否使用无连接线样式|`boolean`|`false`|
|small|是否使用小型步骤条|`boolean`|`false`|
|changeable|是否可以点击切换|`boolean`|`false`|
### `<steps>` 事件

|事件名|描述|参数|
|---|---|---|
|change|步骤数发生改变时触发|step: `number`<br>ev: `Event`|




### `<step>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|title|步骤的标题|`string`|`-`|
|description|步骤的描述信息|`string`|`-`|
|status|步骤的状态|`'wait' \| 'process' \| 'finish' \| 'error'`|`-`|
|disabled|是否禁用|`boolean`|`false`|
### `<step>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|node|节点|step: `number`<br>status: `string`|
|icon|图标|step: `number`<br>status: `string`|
|description|描述内容|-|
