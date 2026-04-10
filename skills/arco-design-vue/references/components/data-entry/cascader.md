---
name: arco-vue-cascader
description: "Arco Design Vue 级联选择 Cascader 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-cascader>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 级联选择 Cascader

来源组件：上游 `web-vue/components/cascader`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-cascader>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
级联选择器的基本用法。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-cascader :options="options" :style="{width:'320px'}" placeholder="Please select ..." />
    <a-cascader :options="options" default-value="datunli" expand-trigger="hover" :style="{width:'320px'}" placeholder="Please select ..." />
  </a-space>
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      options
    }
  },
}
</script>
```

## 示例：允许清除

### 说明
允许清除。




```vue
<template>
  <a-cascader :options="options" v-model="value" :style="{width:'320px'}" placeholder="Please select ..."
              allow-clear />
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref('datunli');

    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      value,
      options
    }
  },
}
</script>
```

## 示例：禁用选项

### 说明
指定 `option` 的 `disabled` 为 `true`，可以禁用该选项。




```vue
<template>
  <a-cascader :options="options" :style="{width:'320px'}" placeholder="Please select ..." />
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
            disabled: true
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
                disabled: true
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      options
    }
  },
}
</script>
```

## 示例：自定义输入框的展示值

### 说明
利用 `formatLabel` 对显示的内容进行自定义处理。




```vue

<template>
  <a-cascader :options="options" default-value="datunli" :style="{width:'320px'}" placeholder="Please select ..." :format-label="format" />
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];

    const format = (options) => {
      const labels = options.map(option => option.label)
      return labels.join('-')
    }

    return {
      options,
      format
    }
  },
}
</script>
```

## 示例：多选模式

### 说明
通过设置 `multiple` 开启多选模式。




```vue
<template>
  <a-cascader :options="options" :default-value="['datunli']" :style="{width:'320px'}" placeholder="Please select ..." multiple/>
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      options
    }
  },
}
</script>
```

## 示例：严格选择模式

### 说明
设置属性 `check-strictly`，开启严格选择模式，点击任何结点都可以选择。多选时将会解除父子节点的关联。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-cascader :options="options" default-value="beijing" :style="{width:'320px'}" placeholder="Please select ..." check-strictly />
    <a-cascader :options="options" :default-value="['beijing']" :style="{width:'320px'}" placeholder="Please select ..." multiple check-strictly />
  </a-space>
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
            disabled: true
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      options
    }
  },
}
</script>
```

## 示例：加载中

### 说明
选择框和下拉菜单显示加载中状态。




```vue
<template>
  <a-cascader :options="[]" :style="{width:'320px'}" placeholder="Please select ..." loading />
</template>
```

## 示例：子选项懒加载

### 说明
通过 `load-more` 属性可以开启数据懒加载功能。
开启数据懒加载功能后，需要在叶子节点标注 `isLeaf: true`，没有标注且没有 `children` 属性的节点会认为需要懒加载处理。
`load-more` 属性有提供 `done` 函数进行回调，可以在回调中传入懒加载的子数据。如果 `done` 函数没有传入数据会认为懒加载失败，此节点可以再次触发懒加载。




```vue
<template>
  <a-space>
    <a-cascader :options="options" :style="{width:'320px'}" placeholder="Please select ..." :load-more="loadMore"/>
  </a-space>
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
          },
          {
            value: 'haidian',
            label: 'Haidian',
            isLeaf: true
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
            isLeaf: true
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
            isLeaf: true
          },
        ],
      },
    ];
    const loadMore = (option, done) => {
      window.setTimeout(() => {
        const nodes = [{
          value: `${option.value}-option1`,
          label: `${option.label}-Option1`,
          isLeaf: true
        }, {
          value: `${option.value}-option2`,
          label: `${option.label}-Option2`,
          isLeaf: true
        }]
        done(nodes)
      }, 2000)
    };

    return {
      options,
      loadMore
    }
  },
}
</script>
```

## 示例：允许搜索

### 说明
通过设置 `allow-search` 让输入框支持搜索功能。




```vue
<template>
  <a-cascader :options="options" :style="{width:'320px'}" placeholder="Please select ..." allow-search/>
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      options
    }
  },
}
</script>
```

## 示例：路径模式

### 说明
`modelValue` 使用路径作为值。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-cascader :options="options" :style="{width:'320px'}" placeholder="Please select ..." path-mode
                @change="handleChange" />
    <a-cascader :options="options"
                :default-value="[['beijing','chaoyang','datunli']]"
                :style="{width:'320px'}"
                placeholder="Please select ..."
                path-mode
                @change="handleChange" />
  </a-space>
</template>

<script>
export default {
  setup() {
    const handleChange = (path) => {
      console.log(path)
    }

    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      options,
      handleChange
    }
  },
}
</script>
```

## 示例：回退选项

### 说明
组件默认会展示在选项中不存在的值，可通过 `fallback` 自定义展示或者关闭




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-cascader :options="options" v-model="value" :style="{width:'320px'}" placeholder="Please select ..." multiple />
    <a-cascader :options="options" v-model="value2" :style="{width:'320px'}"
                placeholder="Please select ..." path-mode multiple :fallback="fallback" />
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref(['datunli', 'wuhou']);
    const value2 = ref([['beijing', 'chaoyang', 'datunli'], ['sichuan', 'chengdu', 'wuhou']]);
    const fallback = (value) => {
      return value.map(item => item.toUpperCase()).join('-')
    }

    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      options,
      value,
      value2,
      fallback
    }
  },
}
</script>
```

## 示例：自定义字段名

### 说明
可以通过 `field-names` 属性自定义 `options` 中数据的格式。




```vue
<template>
  <a-cascader :options="options" :field-names="fieldNames" :style="{width:'320px'}"
            placeholder="Please select ..." />
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const fieldNames = {value: 'city', label: 'text'}
    const options = reactive([
      {
        city: 'beijing',
        text: 'Beijing',
        children: [
          {
            city: 'chaoyang',
            text: 'ChaoYang',
            children: [
              {
                city: 'datunli',
                text: 'Datunli',
              },
            ],
          },
          {
            city: 'haidian',
            text: 'Haidian',
          },
          {
            city: 'dongcheng',
            text: 'Dongcheng',
          },
          {
            city: 'xicheng',
            text: 'Xicheng',
            children: [
              {
                city: 'jinrongjie',
                text: 'Jinrongjie',
              },
              {
                city: 'tianqiao',
                text: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        city: 'shanghai',
        text: 'Shanghai',
        children: [
          {
            city: 'huangpu',
            text: 'Huangpu',
          },
        ],
      },
    ]);

    return {
      fieldNames,
      options
    }
  }
}
</script>
```

## 示例：展开子菜单

### 说明
通过设置 `expand-child` 可以在选择时展开第一个子菜单




```vue
<template>
  <a-cascader :options="options" :style="{width:'320px'}" placeholder="Please select ..." expand-child/>
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      options
    }
  },
}
</script>
```

## 示例：级联菜单

### 说明
级联菜单可以单独使用，此时为 `数据展示` 组件




```vue
<template>
  <a-cascader-panel :options="options" v-model="value" expand-child/>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref('');

    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'huangpu',
            label: 'Huangpu',
          },
        ],
      },
    ];
    return {
      value,
      options
    }
  },
}
</script>
```

## 示例：虚拟列表

### 说明
虚拟列表的使用方法。




```vue

<template>
  <a-cascader :options="options" :style="{width:'320px'}" placeholder="Please select ..."
              :virtual-list-props="{height:200}" />
</template>

<script>
export default {
  setup() {
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'Xicheng',
            children: [
              {
                value: 'jinrongjie',
                label: 'Jinrongjie',
              },
              {
                value: 'tianqiao',
                label: 'Tianqiao',
              },
            ],
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: Array(1000).fill(null).map((_, index) => {
          return {
            value: `Option ${index}`,
            label: `Option ${index}`
          }
        })
      },
    ];

    return {
      options
    }
  },
}
</script>
```

## API


### `<cascader>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|path-mode|绑定值是否为路径|`boolean`|`false`||
|multiple|是否为多选状态（多选模式默认开启搜索）|`boolean`|`false`||
|model-value **(v-model)**|绑定值|`string\| number\| Record<string, any>\| (    \| string    \| number    \| Record<string, any>    \| (string \| number \| Record<string, any>)[]  )[]\| undefined`|`-`||
|default-value|默认值（非受控状态）|`string\| number\| Record<string, any>\| (    \| string    \| number    \| Record<string, any>    \| (string \| number \| Record<string, any>)[]  )[]\| undefined`|`'' \| undefined \| []`||
|options|级联选择器的选项|`CascaderOption[]`|`[]`||
|disabled|是否禁用|`boolean`|`false`||
|error|是否为错误状态|`boolean`|`false`||
|size|选择框的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|allow-search|是否允许搜索|`boolean`|`false (single) \| true (multiple)`||
|allow-clear|是否允许清除|`boolean`|`false`||
|input-value **(v-model)**|输入框的值|`string`|`-`||
|default-input-value|输入框的默认值（非受控状态）|`string`|`''`||
|popup-visible **(v-model)**|是否显示下拉框|`boolean`|`-`||
|expand-trigger|展开下一级的触发方式|`'click' \| 'hover'`|`'click'`||
|default-popup-visible|是否默认显示下拉框（非受控状态）|`boolean`|`false`||
|placeholder|占位符|`string`|`-`||
|filter-option|自定义选项过滤方法|`(inputValue: string, option: CascaderOption) => boolean`|`-`||
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`-`||
|max-tag-count|多选模式下，最多显示的标签数量。0 表示不限制|`number`|`0`||
|format-label|格式化展示内容|`(options: CascaderOption[]) => string`|`-`||
|trigger-props|下拉菜单的触发器属性|`TriggerProps`|`-`||
|check-strictly|是否开启严格选择模式|`boolean`|`false`||
|load-more|数据懒加载函数，传入时开启懒加载功能|`(  option: CascaderOption,  done: (children?: CascaderOption[]) => void) => void`|`-`|2.13.0|
|loading|是否为加载中状态|`boolean`|`false`|2.15.0|
|search-option-only-label|搜索下拉菜单中的选项是否仅展示标签|`boolean`|`false`|2.18.0|
|search-delay|触发搜索事件的延迟时间|`number`|`500`|2.18.0|
|field-names|自定义 `CascaderOption` 中的字段|`CascaderFieldNames`|`-`|2.22.0|
|value-key|用于确定选项键值的属性名|`string`|`'value'`|2.29.0|
|fallback|自定义不存在选项的值的展示|`boolean\| ((    value:      \| string      \| number      \| Record<string, unknown>      \| (string \| number \| Record<string, unknown>)[]  ) => string)`|`true`|2.29.0|
|expand-child|是否展开子菜单|`boolean`|`false`|2.29.0|
|virtual-list-props|传递虚拟列表属性，传入此参数以开启虚拟滚动 [VirtualListProps](#VirtualListProps)|`VirtualListProps`|`-`|2.49.0|
|tag-nowrap|标签内容不换行|`boolean`|`false`|2.56.1|
### `<cascader>` 事件

|事件名|描述|参数|
|---|---|---|
|change|选中值改变时触发|value: `string \| number \| (string \| number \| (string \| number)[])[] \| undefined`|
|input-value-change|输入值改变时触发|value: `string`|
|clear|点击清除按钮时触发|-|
|search|用户搜索时触发|value: `string`|
|popup-visible-change|下拉框的显示状态改变时触发|visible: `boolean`|
|focus|获得焦点时触发|ev: `FocusEvent`|
|blur|失去焦点时触发|ev: `FocusEvent`|
### `<cascader>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|label|选择框的显示内容|data: `CascaderOption`|2.18.0|
|prefix|前缀元素|-|2.23.0|
|arrow-icon|选择框的箭头图标|-|2.16.0|
|loading-icon|选择框的加载中图标|-|2.16.0|
|search-icon|选择框的搜索图标|-|2.16.0|
|empty|选项为空时的显示内容|-|2.23.0|
|option|选项内容|data: `CascaderOption`|2.18.0|




### `<cascader-panel>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|path-mode|绑定值是否为路径|`boolean`|`false`||
|multiple|是否为多选状态（多选模式默认开启搜索）|`boolean`|`false`||
|model-value **(v-model)**|绑定值|`string\| number\| Record<string, any>\| (    \| string    \| number    \| Record<string, any>    \| (string \| number \| Record<string, any>)[]  )[]\| undefined`|`-`||
|default-value|默认值（非受控状态）|`string\| number\| Record<string, any>\| (    \| string    \| number    \| Record<string, any>    \| (string \| number \| Record<string, any>)[]  )[]\| undefined`|`'' \| undefined \| []`||
|options|级联选择器的选项|`CascaderOption[]`|`[]`||
|expand-trigger|展开下一级的触发方式|`string`|`'click'`||
|check-strictly|是否开启严格选择模式|`boolean`|`false`||
|load-more|数据懒加载函数，传入时开启懒加载功能|`(  option: CascaderOption,  done: (children?: CascaderOption[]) => void) => void`|`-`|2.13.0|
|field-names|自定义 `CascaderOption` 中的字段|`CascaderFieldNames`|`-`|2.22.0|
|value-key|用于确定选项键值的属性名|`string`|`'value'`|2.29.0|
|expand-child|是否展开子菜单|`boolean`|`false`|2.29.0|
### `<cascader-panel>` 事件

|事件名|描述|参数|
|---|---|---|
|change|选中值改变时触发|value: `string \| number \| (string \| number \| (string \| number)[])[] \| undefined`|
### `<cascader-panel>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|empty|选项为空时的显示内容|-|2.23.0|




### CascaderOption

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|value|选项值，2.29.0 版本支持对象|`string \| number \| Record<string, any>`|`-`||
|label|选项文本|`string`|`-`||
|render|自定义渲染|`RenderFunction`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|tagProps|展示的标签属性|`TagProps`|`-`|2.8.0|
|children|下一级选项|`CascaderOption[]`|`-`||
|isLeaf|是否是叶子节点|`boolean`|`false`||
