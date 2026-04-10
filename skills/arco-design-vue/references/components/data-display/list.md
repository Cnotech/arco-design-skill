---
name: arco-vue-list
description: "Arco Design Vue 列表 List 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-list>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 列表 List

来源组件：上游 `web-vue/components/list`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-list>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
列表的基本使用方法。可用于承载文字、列表、图片和段落。




```vue
<template>
  <a-list>
    <template #header>
      List title
    </template>
    <a-list-item>Beijing Bytedance Technology Co., Ltd.</a-list-item>
    <a-list-item>Bytedance Technology Co., Ltd.</a-list-item>
    <a-list-item>Beijing Toutiao Technology Co., Ltd.</a-list-item>
    <a-list-item>Beijing Volcengine Technology Co., Ltd.</a-list-item>
    <a-list-item>China Beijing Bytedance Technology Co., Ltd.</a-list-item>
  </a-list>
</template>
```

## 示例：不同尺寸

### 说明
列表组件提供了三种大小 `small, medium, large` ，可根据业务需求自行选择。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-radio-group v-model="size" type="button">
      <a-radio value="small">Small</a-radio>
      <a-radio value="medium">Medium</a-radio>
      <a-radio value="large">Large</a-radio>
    </a-radio-group>
    <a-list :size="size">
      <template #header>
        List title
      </template>
      <a-list-item>Beijing Bytedance Technology Co., Ltd.</a-list-item>
      <a-list-item>Bytedance Technology Co., Ltd.</a-list-item>
      <a-list-item>Beijing Toutiao Technology Co., Ltd.</a-list-item>
      <a-list-item>Beijing Volcengine Technology Co., Ltd.</a-list-item>
      <a-list-item>China Beijing Bytedance Technology Co., Ltd.</a-list-item>
    </a-list>
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const size = ref('medium');

    return {
      size
    }
  },
}
</script>
```

## 示例：列表元素

### 说明
使用 `list-item-meta` 组件可快速指定头像、标题、文字。




```vue
<template>
  <a-list>
    <a-list-item v-for="idx in 4" :key="idx">
      <a-list-item-meta
        title="Beijing Bytedance Technology Co., Ltd."
        description="Beijing ByteDance Technology Co., Ltd. is an enterprise located in China."
      >
        <template #avatar>
          <a-avatar shape="square">
            <img
              alt="avatar"
              src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp"
            />
          </a-avatar>
        </template>
      </a-list-item-meta>
    </a-list-item>
  </a-list>
</template>
```

## 示例：增加操作项

### 说明
通过 `actions` 来为列表添加操作项。




```vue
<template>
  <a-list>
    <a-list-item v-for="idx in 4" :key="idx">
      <a-list-item-meta
        title="Beijing Bytedance Technology Co., Ltd."
        description="Beijing ByteDance Technology Co., Ltd. is an enterprise located in China."
      >
        <template #avatar>
          <a-avatar shape="square">
            <img
              alt="avatar"
              src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp"
            />
          </a-avatar>
        </template>
      </a-list-item-meta>
      <template #actions>
        <icon-edit />
        <icon-delete />
      </template>
    </a-list-item>
  </a-list>
</template>
```

## 示例：竖排列表样式

### 说明
这是一个包括分页、右侧内容、下方列表操作的示例。




```vue
<template>
  <a-list
    class="list-demo-action-layout"
    :bordered="false"
    :data="dataSource"
    :pagination-props="paginationProps"
  >
    <template #item="{ item }">
      <a-list-item class="list-demo-item" action-layout="vertical">
        <template #actions>
          <span><icon-heart />83</span>
          <span><icon-star />{{ item.index }}</span>
          <span><icon-message />Reply</span>
        </template>
        <template #extra>
          <div className="image-area">
            <img alt="arco-design" :src="item.imageSrc" />
          </div>
        </template>
        <a-list-item-meta
          :title="item.title"
          :description="item.description"
        >
          <template #avatar>
            <a-avatar shape="square">
              <img alt="avatar" :src="item.avatar" />
            </a-avatar>
          </template>
        </a-list-item-meta>
      </a-list-item>
    </template>
  </a-list>
</template>

<script>
import { reactive } from 'vue'

const names = ['Socrates', 'Balzac', 'Plato'];
const avatarSrc = [
  '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp',
  '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/e278888093bef8910e829486fb45dd69.png~tplv-uwbnlip3yd-webp.webp',
  '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/9eeb1800d9b78349b24682c3518ac4a3.png~tplv-uwbnlip3yd-webp.webp',
];
const imageSrc = [
  '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/29c1f9d7d17c503c5d7bf4e538cb7c4f.png~tplv-uwbnlip3yd-webp.webp',
  '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/04d7bc31dd67dcdf380bc3f6aa07599f.png~tplv-uwbnlip3yd-webp.webp',
  '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/1f61854a849a076318ed527c8fca1bbf.png~tplv-uwbnlip3yd-webp.webp',
];
const dataSource = new Array(15).fill(null).map((_, index) => {
  return {
    index: index,
    avatar: avatarSrc[index % avatarSrc.length],
    title: names[index % names.length],
    description:
      'Beijing ByteDance Technology Co., Ltd. is an enterprise located in China. ByteDance has products such as TikTok, Toutiao, volcano video and Douyin (the Chinese version of TikTok).',
    imageSrc: imageSrc[index % imageSrc.length],
  };
});

export default {
  setup() {
    return {
      dataSource,
      paginationProps: reactive({
        defaultPageSize: 3,
        total: dataSource.length
      })
    }
  },
}
</script>

<style scoped>
.list-demo-action-layout .image-area {
  width: 183px;
  height: 119px;
  border-radius: 2px;
  overflow: hidden;
}

.list-demo-action-layout .list-demo-item {
  padding: 20px 0;
  border-bottom: 1px solid var(--color-fill-3);
}

.list-demo-action-layout .image-area img {
  width: 100%;
}

.list-demo-action-layout .arco-list-item-action .arco-icon {
  margin: 0 4px;
}
</style>
```

## 示例：格栅列表

### 说明
通过 `grid` 属性来配置格栅列表。




```vue
<template>
  <a-list :gridProps="{ gutter: 0, span: 6 }" :bordered="false">
    <a-list-item>
      <a-list>
        <template #header>Platform</template>
        <a-list-item>iOS</a-list-item>
        <a-list-item>Android</a-list-item>
        <a-list-item>Web</a-list-item>
      </a-list>
    </a-list-item>
    <a-list-item>
      <a-list>
        <template #header>Framework</template>
        <a-list-item>Angular</a-list-item>
        <a-list-item>Vue</a-list-item>
        <a-list-item>React</a-list-item>
      </a-list>
    </a-list-item>
    <a-list-item>
      <a-list>
        <template #header>Language</template>
        <a-list-item>C++</a-list-item>
        <a-list-item>JavaScript</a-list-item>
        <a-list-item>Python</a-list-item>
      </a-list>
    </a-list-item>
    <a-list-item>
      <a-list>
        <template #header>Component</template>
        <a-list-item>Button</a-list-item>
        <a-list-item>Breadcrumb</a-list-item>
        <a-list-item>Transfer</a-list-item>
      </a-list>
    </a-list-item>
  </a-list>
</template>
```

## 示例：响应式栅格

### 说明
通过 `grid.sm` 等响应式参数动态设置每个单项横跨的列数，注意此时不要设置 `grid.span`。




```vue
<template>
  <a-list
    :grid-props="{ gutter: [20, 20], sm: 24, md: 12, lg: 8, xl: 6 }"
    :data="dataSource"
    :bordered="false"
  >
    <template #item="{ item }">
      <a-list :data="item.data">
        <template #header>{{ item.title }}</template>
        <template #item="{ item: subItem }">
          <a-list-item>{{ subItem }}</a-list-item>
        </template>
      </a-list>
    </template>
  </a-list>
</template>

<script>
const dataSource = [
  {
    title: 'Platform',
    data: ['iOS', 'Android', 'Web'],
  },
  {
    title: 'Framework',
    data: ['Angular', 'Vue', 'React'],
  },
  {
    title: 'Language',
    data: ['C++', 'JavaScript', 'Python'],
  },
  {
    title: 'Component',
    data: ['Button', 'Breadcrumb', 'Transfer'],
  },
  {
    title: 'Design',
    data: ['Figma', 'Sketch', 'Adobe XD'],
  },
  {
    title: 'Plugin',
    data: ['Edu Tools', 'BashSupport', 'GitToolBox'],
  },
  {
    title: 'Platform',
    data: ['iOS', 'Android', 'Web'],
  },
  {
    title: 'Framework',
    data: ['Angular', 'Vue', 'React'],
  },
  {
    title: 'Language',
    data: ['C++', 'JavaScript', 'Python'],
  },
];

export default {
  setup() {
    return {
      dataSource
    }
  }
}
</script>
```

## 示例：滚动

### 说明
通过设置 `max-height` 属性限制列表的最大高度。通过 `reach-bottom` 事件可以监听列表触底的事件。




```vue
<template>
  <div style="margin-bottom: 10px">
    <a-switch v-model="scrollbar" />
    Virtual Scrollbar
  </div>
  <a-list :max-height="240" @reach-bottom="fetchData" :scrollbar="scrollbar">
    <template #header>
      List title
    </template>
    <template #scroll-loading>
      <div v-if="bottom">No more data</div>
      <a-spin v-else />
    </template>
    <a-list-item v-for="item of data">{{item}}</a-list-item>
  </a-list>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const current = ref(1);
    const bottom = ref(false);
    const data = reactive([]);
    const scrollbar = ref(true);

    const fetchData = () => {
      console.log('reach bottom!');
      if (current.value <= 5) {
        window.setTimeout(() => {
          const index = data.length;
          data.push(
            `Beijing Bytedance Technology Co., Ltd. ${index + 1}`,
            `Bytedance Technology Co., Ltd. ${index + 2}`,
            `Beijing Toutiao Technology Co., Ltd. ${index + 3}`,
            `Beijing Volcengine Technology Co., Ltd. ${index + 4}`,
            `China Beijing Bytedance Technology Co., Ltd. ${index + 5}`
          );
          current.value += 1
        }, 2000)
      } else {
        bottom.value = true
      }
    }

    return {
      current,
      bottom,
      data,
      fetchData,
      scrollbar
    }
  },
}
</script>
```

## 示例：无限长列表

### 说明
通过指定 `virtualListProps` 来开启虚拟列表，在大量数据时获得高性能表现。
在使用虚拟列表时，如果列表元素之间高度变化较大可能导致滚动时视口出现空白区域，可通过调整 `virtualListProps.buffer` 属性解决，[使用方式](/vue/docs/faq#%E8%99%9A%E6%8B%9F%E5%88%97%E8%A1%A8%E7%9A%84%E4%BD%BF%E7%94%A8)。




```vue

<template>
  <h3 :style="{ color: 'var(--color-text-2)' }">10000 items</h3>
  <a-list
    :style="{ width: `600px` }"
    :virtualListProps="{
      height: 560,
    }"
    :data="list"
  >
    <template #item="{ item, index }">
      <a-list-item :key="index">
        <a-list-item-meta
          :title="item.title"
          :description="item.description"
        >
          <template #avatar>
            <a-avatar shape="square">
              A
            </a-avatar>
          </template>
        </a-list-item-meta>
      </a-list-item>
    </template>
  </a-list>
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const list = reactive(Array(10000).fill(null).map((_, index) => {
      const prefix = `0000${index}`.slice(-5);
      return {
        title: 'Beijing Bytedance Technology Co., Ltd.',
        description: `(${prefix}) Beijing ByteDance Technology Co., Ltd. is an enterprise located in China.`,
      };
    }))

    return {
      list
    }
  },
}
</script>
```

## API


### `<list>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|data|列表数据，需要和 `item` 插槽同时使用|`any[]`|`-`||
|size|列表大小|`'small' \| 'medium' \| 'large'`|`'medium'`||
|bordered|是否显示边框|`boolean`|`true`||
|split|是否显示分割线|`boolean`|`true`||
|loading|是否为加载中状态|`boolean`|`false`||
|hoverable|是否显示选中样式|`boolean`|`false`||
|pagination-props|列表分页配置|`PaginationProps`|`-`||
|grid-props|列表栅格配置|`object`|`-`||
|max-height|列表的最大高度|`string \| number`|`0`||
|bottom-offset|触发到达底部的距离阈值|`number`|`0`||
|virtual-list-props|传递虚拟列表属性，传入此参数以开启虚拟滚动 [VirtualListProps](#VirtualListProps)|`VirtualListProps`|`-`||
|scrollbar|是否开启虚拟滚动条|`boolean \| ScrollbarProps`|`true`|2.38.0|
### `<list>` 事件

|事件名|描述|参数|
|---|---|---|
|scroll|列表滚动时触发|-|
|reach-bottom|当列表到达底部时触发|-|
|page-change|表格分页发生改变时触发|page: `number`|
|page-size-change|表格每页数据数量发生改变时触发|pageSize: `number`|
### `<list>` 方法

|方法名|描述|参数|返回值|
|---|---|---|---|
|scrollIntoView|虚拟滚动到某个元素|options: `{ index?: number; key?: number \| string; align: 'auto' \| 'top' \| 'bottom'}`|-|
### `<list>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|scroll-loading|滚动加载状态时，滚动到底部的提示|-|2.20.0|
|item|列表项|index: `number`<br>item: `any`||
|empty|空白展示|-||
|footer|底部信息|-||
|header|头部信息|-||




### `<list-item>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|action-layout|操作组排列方向|`Direction`|`'horizontal'`|
### `<list-item>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|meta|meta信息|-|
|extra|额外内容|-|
|actions|操作组|-|




### `<list-item-meta>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|title|标题|`string`|`-`|
|description|描述内容|`string`|`-`|
### `<list-item-meta>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|avatar|头像|-|
|title|标题|-|
|description|描述内容|-|




### VirtualListProps

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|height|可视区域高度|`number \| string`|`-`||
|threshold|开启虚拟滚动的元素数量阈值，当数据数量小于阈值时不会开启虚拟滚动。|`number`|`-`||
|isStaticItemHeight|（已废除）元素高度是否是固定的。2.34.1 版本废除，请使用 `fixedSize`|`boolean`|`false`||
|fixedSize|元素高度是否是固定的。|`boolean`|`false`|2.34.1|
|estimatedSize|元素高度不固定时的预估高度。|`number`|`-`|2.34.1|
|buffer|视口边界外提前挂载的元素数量。|`number`|`10`|2.34.1|
