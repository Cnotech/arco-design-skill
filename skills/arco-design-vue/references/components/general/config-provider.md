---
name: arco-vue-config-provider
description: "Arco Design Vue 全局配置 ConfigProvider 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-config-provider>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 全局配置 ConfigProvider

来源组件：上游 `web-vue/components/config-provider`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-config-provider>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
设置国际化语言的基本用法。




```vue
<template>
  <a-config-provider :locale="locale">
    <a-radio-group
      type="button"
      v-model="localeType"
      :options="localeOptions"
    ></a-radio-group>
    <div>
      <a-pagination
        :total="50"
        show-total
        show-jumper
        show-page-size
        style="margin-top: 20px; margin-bottom: 20px;"
      />
    </div>
    <a-space :size="20" style="margin-bottom: 20px;">
      <a-range-picker style="width: 300px;" />
      <a-time-picker type="time-range" style="width: 300px;" />
      <a-popconfirm content="Are you sure you want to delete?">
        <a-button type="primary">Popconfirm</a-button>
      </a-popconfirm>
    </a-space>
  </a-config-provider>
</template>

<script>
import { ref, computed } from 'vue';
import zhCN from '@arco-design/web-vue/es/locale/lang/zh-cn';
import enUS from '@arco-design/web-vue/es/locale/lang/en-us';
import esES from '@arco-design/web-vue/es/locale/lang/es-es';
import jaJP from '@arco-design/web-vue/es/locale/lang/ja-jp';
import idID from '@arco-design/web-vue/es/locale/lang/id-id';
import frFR from '@arco-design/web-vue/es/locale/lang/fr-fr';
import ptPT from '@arco-design/web-vue/es/locale/lang/pt-pt';
import deDE from '@arco-design/web-vue/es/locale/lang/de-de';
import koKR from '@arco-design/web-vue/es/locale/lang/ko-kr';
import itIT from '@arco-design/web-vue/es/locale/lang/it-it';
import thTH from '@arco-design/web-vue/es/locale/lang/th-th';
import viVN from '@arco-design/web-vue/es/locale/lang/vi-vn';
import nlNL from '@arco-design/web-vue/es/locale/lang/nl-nl';

const locales = {
  'zh-CN': zhCN,
  'en-US': enUS,
  'es-ES': esES,
  'ja-JP': jaJP,
  'id-ID': idID,
  'fr-FR': frFR,
  'pt-PT': ptPT,
  'de-DE': deDE,
  'ko-KR': koKR,
  'it-IT': itIT,
  'th-TH': thTH,
  'vi-VN': viVN,
  'nl-NL': nlNL,
};

export default {
  setup() {
    const localeType = ref('es-ES');
    const locale = computed(() => {
      return locales[localeType.value] || zhCN;
    });

    return {
      localeType,
      locale,
      localeOptions: Object.keys(locales),
    };
  },
};
</script>
```

## 示例：自定义空状态元素

### 说明
通过 `empty` 插槽可以全局自定义空状态元素。




```vue
<template>
  <a-config-provider>
    <template #empty="scope">
      <a-empty v-if="scope?.component==='cascader'" description="cascader no data!" in-config-provider>
      </a-empty>
      <a-empty v-else-if="scope?.component==='select'" description="select no data!" in-config-provider></a-empty>
      <a-empty v-else-if="scope?.component==='tree-select'" description="tree-select no data!" in-config-provider></a-empty>
      <a-empty v-else-if="scope?.component==='list'" description="list no data!" in-config-provider></a-empty>
      <a-empty v-else-if="scope?.component==='table'" description="table no data!" in-config-provider></a-empty>
      <div v-else class="my-empty">
        <icon-trophy />
      </div>
    </template>
    <a-space direction="vertical" fill>
      <a-cascader :options="[]" placeholder="cascader" allow-search />
      <a-select placeholder="select" allow-search />
      <a-tree-select placeholder="tree-select"/>
      <a-list>
        <template #header>
          Empty List
        </template>
      </a-list>
      <a-table :columns="columns" :data="[]" />
      <a-empty></a-empty>
    </a-space>
  </a-config-provider>
</template>

<script>
import { IconTrophy } from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconTrophy
  },
  setup() {
    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
      },
      {
        title: 'Salary',
        dataIndex: 'salary',
      },
      {
        title: 'Address',
        dataIndex: 'address',
      },
      {
        title: 'Email',
        dataIndex: 'email',
      },
    ];
    return {
      columns
    }
  }
}
</script>

<style>
.my-empty {
  padding: 20px;
  width: 100%;
  text-align: center;
  box-sizing: border-box;
}
</style>
```

## 示例：RTL 视图

### 说明
设置组件为从右向左阅读的视图。




```vue
<template>
  <div>
    <a-switch v-model="rtlType" style="margin-bottom: 20px;">
      <template #checked>
        RTL
      </template>
      <template #unchecked>
        LTR
      </template>
    </a-switch>
    <a-config-provider :rtl="rtlType">
      <a-tabs :default-active-key="2" style="margin-bottom: 20px;">
        <a-tab-pane
          v-for="i in 36"
          :key="i"
          :title="`Tab ${i}`"
        >
          Content of Tab Panel {{ i }}
        </a-tab-pane>
      </a-tabs>
      <a-space :direction="'vertical'" style="width: 100%;">
        <a-space :size="40">
          <a-badge :count="9">
            <a-avatar shape="square" />
          </a-badge>
          <a-badge :count="9" dot :dotStyle="{ width: '10px', height: '10px' }">
            <a-avatar shape="square" />
          </a-badge>
          <a-badge :dotStyle="{ height: '16px', width: '16px', fontSize: '14px' }">
            <template #content>
              <IconClockCircle
                :style="{ verticalAlign: 'middle', color: 'var(--color-text-2)' }"
              />
            </template>
            <a-avatar shape="square" />
          </a-badge>
          <a-tag :color="'red'" closable>red</a-tag>
          <a-tag :color="'blue'" closable>blue</a-tag>
          <a-tag :color="'green'" closable>green</a-tag>
        </a-space>
      </a-space>
    </a-config-provider>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const rtlType = ref(true);

    return {
      rtlType,
    };
  },
};
</script>
```

## API


### `<config-provider>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|prefix-cls|组件类名前缀|`string`|`'arco'`||
|locale|配置语言包|`ArcoLang`|`-`||
|size|大小|`Size`|`-`|2.14.0|
|global|是否全局生效|`boolean`|`false`|2.25.0|
|update-at-scroll|是否在容器滚动时更新弹出框的位置|`boolean`|`false`|2.25.0|
|scroll-to-close|是否在滚动时关闭弹出框|`boolean`|`false`|2.46.0|
|exchange-time|是否交换时间|`boolean`|`true`|2.48.0|
|rtl|视图的表现形式是从右开始向左结束|`boolean`|`false`||
### `<config-provider>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|loading|自定义加载中元素|-|2.28.0|
|empty|自定义空状态元素|component: `string`|2.28.0|




## FAQ

### 全局配置

`global` 属性设置为 `true` 时，会将配置内容注入到 Vue AppContext 中，一般用于解决使用 Modal、Message 组件的函数式调用方法时，配置内容无法生效的问题。

### 自定义空状态展示

可以在 `#empty` 中自定义组件库全局的空状态展示，如果在插槽中使用到了 `Empty` 组件，需要开启 `inConfigProvider` 属性。
