---
name: arco-vue-select
description: "Arco Design Vue 选择器 Select 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-select>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 选择器 Select

来源组件：上游 `web-vue/components/select`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-select>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
选择器的基本用法。
通过 `trigger-props` 属性自定义下拉框的属性，比如可以让下拉框自动适应最小宽度。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-select :style="{width:'320px'}" placeholder="Please select ...">
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
    </a-select>
    <a-select :style="{width:'320px'}" placeholder="Please select ...">
      <a-option :value="true">是</a-option>
      <a-option :value="false">否</a-option>
    </a-select>
    <a-select defaultValue="Beijing" :style="{width:'320px'}" placeholder="Please select ..." disabled>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
    </a-select>
    <a-select v-model="value" :style="{width:'320px'}" placeholder="Please select ...">
      <a-option v-for="item of data" :value="item" :label="item.label" />
    </a-select>
    <div>Select Value: {{ value }}</div>
    <a-select :style="{width:'160px'}" placeholder="Select" :trigger-props="{ autoFitPopupMinWidth: true }">
      <a-option>Beijing-Beijing-Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
    </a-select>
    
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref();
    const data = [{
      value: 'beijing',
      label: 'Beijing',
      other: 'extra'
    }, {
      value: 'shanghai',
      label: 'Shanghai',
      other: 'extra'
    }, {
      value: 'guangzhou',
      label: 'Guangzhou',
      other: 'extra'
    }, {
      value: 'chengdu',
      label: 'Chengdu',
      other: 'extra'
    }]

    return {
      value,
      data
    }
  },
}
</script>
```

## 示例：允许清除

### 说明
通过设置 `allow-clear` ，显示清除按钮。




```vue

<template>
  <a-select :style="{width:'320px'}" v-model="value" placeholder="Please select ..." allow-clear>
    <a-option>Beijing</a-option>
    <a-option>Shanghai</a-option>
    <a-option>Guangzhou</a-option>
    <a-option disabled>Disabled</a-option>
  </a-select>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref('Shanghai');
    return {
      value
    }
  },
}
</script>
```

## 示例：多选选择器

### 说明
通过设置 `multiple` ，可以让选择器支持多选。此外通过 `max-tag-count` 可以设置最多显示的标签个数。




```vue

<template>
  <div style="margin-bottom: 10px">
    <a-switch v-model="scrollbar" />
    Virtual Scrollbar
  </div>
  <a-space direction="vertical" size="large">
    <a-select :default-value="['Beijing','Shanghai']" :style="{width:'360px'}" placeholder="Please select ..." multiple
              :scrollbar="scrollbar">
      <a-option>Beijing</a-option>
      <a-option :tag-props="{color:'red'}">Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
    <a-select :default-value="['Beijing','Shanghai','Guangzhou']" :style="{width:'360px'}"
              placeholder="Please select ..." multiple :max-tag-count="2" allow-clear :scrollbar="scrollbar">
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Chengdu</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
    <a-select :default-value="['Beijing','Shanghai']" :style="{width:'360px'}" placeholder="Please select ..." multiple
              :limit="2" :scrollbar="scrollbar">
      <a-option>Beijing</a-option>
      <a-option :tag-props="{color:'red'}">Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
  </a-space>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const scrollbar = ref(true);

    return {
      scrollbar
    }
  }
}
</script>
```

## 示例：选择框大小

### 说明
选择框分为 `mini`、`small`、`medium`、`large` 四种尺寸。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-radio-group type="button" v-model="size">
      <a-radio value="mini">Mini</a-radio>
      <a-radio value="small">Small</a-radio>
      <a-radio value="medium">Medium</a-radio>
      <a-radio value="large">Large</a-radio>
    </a-radio-group>
    <a-select default-value="Beijing" :style="{width:'320px'}" :size="size" placeholder="Please select ...">
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
    </a-select>
    <a-select :default-value="['Beijing','Shanghai']" :style="{width:'320px'}" :size="size"
              placeholder="Please select ..." multiple>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Chengdu</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
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

## 示例：加载中

### 说明
选择框和下拉菜单显示加载中状态。




```vue
<template>
  <a-select :style="{width:'320px'}" placeholder="Please select ..." loading>
    <a-option>Beijing</a-option>
    <a-option>Shanghai</a-option>
    <a-option>Guangzhou</a-option>
    <a-option disabled>Disabled</a-option>
  </a-select>
</template>
```

## 示例：下拉菜单的页头

### 说明
自定义下拉菜单的页头




```vue
<template>
  <a-space>
    <a-select :default-value="'Beijing'" :style="{width:'360px'}" placeholder="Please select ..." multiple>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Wuhan</a-option>
      <template #header>
        <div style="padding: 6px 12px;" >
          <a-checkbox value="1">全选</a-checkbox>
        </div>
      </template>
    </a-select>

    <a-select :default-value="'Beijing'" :style="{width:'360px'}" placeholder="Please select ..." multiple show-header-on-empty>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Wuhan</a-option>
      <template #header>
        <div style="padding: 6px 12px;" >
          <a-checkbox value="1">全选</a-checkbox>
        </div>
      </template>
    </a-select>
  </a-space>
</template>
```

## 示例：下拉菜单的页脚

### 说明
自定义下拉菜单的页脚




```vue
<template>
  <a-space>
    <a-select :default-value="'Beijing'" :style="{width:'360px'}" placeholder="Please select ..." allow-search>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Wuhan</a-option>
      <template #footer>
        <div style="padding: 6px 0; text-align: center;">
          <a-button>Click Me</a-button>
        </div>
      </template>
    </a-select>
    <a-select :default-value="'Beijing'" :style="{width:'360px'}" placeholder="Please select ..." allow-search show-footer-on-empty>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Wuhan</a-option>
      <template #footer>
        <div style="padding: 6px 0; text-align: center;">
          <a-button>Click Me</a-button>
        </div>
      </template>
    </a-select>
  </a-space>
</template>
```

## 示例：无边框模式

### 说明
设置 `bordered="false"` 开启无边框模式，常用于沉浸式使用。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-select :style="{width:'100%'}" placeholder="Please select ..." :bordered="false">
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
    </a-select>
    <a-select :default-value="['Beijing','Shanghai']" :style="{width:'360px'}" placeholder="Please select ..." multiple :bordered="false">
      <a-option>Beijing</a-option>
      <a-option :tag-props="{color:'red'}">Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
  </a-space>
</template>
```

## 示例：允许创建

### 说明
通过设置 `allow-create` ，让选择器可以创建选项中不存在的条目。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-select :style="{width:'320px'}" placeholder="Please select ..." allow-create>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Chengdu</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
    <a-select :style="{width:'320px'}" placeholder="Please select ..." multiple allow-create>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Chengdu</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
  </a-space>
</template>
```

## 示例：允许搜索

### 说明
通过设置 `allow-search` ，可以让选择器支持对选项的搜索，配合 `filter-option` 可以自定义搜索。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-select :style="{width:'320px'}" placeholder="Please select ..." allow-search>
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Chengdu</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
    <a-select :style="{width:'320px'}" placeholder="Please select ..." :allow-search="{ retainInputValue: true }">
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Chengdu</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
    <a-select :options="options" :style="{width:'320px'}" :loading="loading" placeholder="Please select ..." multiple
              @search="handleSearch" />
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const options = ref(['Option1', 'Option2', 'Option3']);
    const loading = ref(false);

    const handleSearch = (value) => {
      if (value) {
        loading.value = true;
        window.setTimeout(() => {
          options.value = [`${value}-Option1`, `${value}-Option2`, `${value}-Option3`]
          loading.value = false;
        }, 2000)
      } else {
        options.value = []
      }
    };

    return {
      options,
      loading,
      handleSearch
    }
  },
}
</script>
```

## 示例：下拉菜单滚动

### 说明
可以通过 `dropdown-scroll` 监听下拉菜单的滚动事件。或者通过 `dropdown-reach-bottom` 监听下拉菜单滚动到底部的事件。




```vue
<template>
  <a-select
    :style="{width:'320px'}"
    default-value="Beijing"
    placeholder="Please select ..."
    @dropdown-scroll="handleScroll"
    @dropdown-reach-bottom="handleReachBottom"
  >
    <a-option>Beijing</a-option>
    <a-option>Shanghai</a-option>
    <a-option>Guangzhou</a-option>
    <a-option disabled>Disabled</a-option>
    <a-option>Shenzhen</a-option>
    <a-option>Chengdu</a-option>
    <a-option>Wuhan</a-option>
  </a-select>
</template>

<script>
export default {
  setup() {
    const handleScroll = (ev) => {
      console.log('scroll', ev)
    }
    const handleReachBottom = (ev) => {
      console.log('reach the bottom', ev)
    }

    return {
      handleScroll,
      handleReachBottom
    }
  },
}
</script>
```

## 示例：回退选项

### 说明
使用 `fallback-option` 自定义选项中不存在的值，默认会在输入框中展示不存在的选项值。可能用于选项还没有获取完，或者远程搜索时选项改变了。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-select defaultValue="Shanxi" :style="{width:'320px'}" placeholder="Please select ..." :fallback-option="fallback">
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
    </a-select>
    <a-select defaultValue="Shanxi" :style="{width:'320px'}" placeholder="Please select ..." :fallback-option="fallback" :show-extra-options="false">
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
    </a-select>
    <a-select :default-value="['Shanxi','Nanjing','Hangzhou']" :style="{width:'320px'}" placeholder="Please select ..." multiple :fallback-option="fallback">
      <a-option>Beijing</a-option>
      <a-option>Shanghai</a-option>
      <a-option>Guangzhou</a-option>
      <a-option disabled>Disabled</a-option>
      <a-option>Shenzhen</a-option>
      <a-option>Chengdu</a-option>
      <a-option>Wuhan</a-option>
    </a-select>
  </a-space>
</template>

<script>
export default {
  setup() {
    const fallback = (value) => {
      return {
        value,
        label: `++${value}++`
      }
    };
    return {
      fallback
    }
  },
}
</script>
```

## 示例：远程搜索

### 说明
使用 `search` 事件进行远程搜索，并改变选项。




```vue

<template>
  <a-space direction="vertical" size="large">
    <div>Show selections after search options</div>
    <a-select :style="{width:'320px'}" :loading="loading" placeholder="Please select ..." multiple
              @search="handleSearch" :filter-option="false">
      <a-option v-for="item of options" :value="item">{{item}}</a-option>
    </a-select>
    <div>Hide selections after search options</div>
    <a-select :options="options" :style="{width:'320px'}" :loading="loading" placeholder="Please select ..." multiple
              @search="handleSearch" :filter-option="false" :show-extra-options="false" />
  </a-space>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const options = ref(['Option1', 'Option2', 'Option3']);
    const loading = ref(false);

    const handleSearch = (value) => {
      if (value) {
        loading.value = true;
        window.setTimeout(() => {
          options.value = [`${value}-Option1`, `${value}-Option2`, `${value}-Option3`]
          loading.value = false;
        }, 2000)
      } else {
        options.value = []
      }
    };

    return {
      options,
      loading,
      handleSearch
    }
  },
}
</script>
```

## 示例：分组

### 说明
使用 `optgroup` 组件添加分组选项。




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-select :style="{width:'320px'}" placeholder="Please select ...">
      <a-optgroup label="Group-1">
        <a-option>Beijing</a-option>
        <a-option>Shanghai</a-option>
      </a-optgroup>
      <a-optgroup label="Group-2">
        <a-option>Guangzhou</a-option>
        <a-option disabled>Disabled</a-option>
        <a-option>Shenzhen</a-option>
      </a-optgroup>
      <a-optgroup label="Group-3">
        <a-option>Chengdu</a-option>
        <a-option>Wuhan</a-option>
      </a-optgroup>
    </a-select>
    <a-select :style="{width:'320px'}" placeholder="Please select ..." multiple>
      <a-optgroup label="Group-1">
        <a-option>Beijing</a-option>
        <a-option>Shanghai</a-option>
      </a-optgroup>
      <a-optgroup label="Group-2">
        <a-option>Guangzhou</a-option>
        <a-option disabled>Disabled</a-option>
        <a-option>Shenzhen</a-option>
      </a-optgroup>
      <a-optgroup label="Group-3">
        <a-option>Chengdu</a-option>
        <a-option>Wuhan</a-option>
      </a-optgroup>
    </a-select>
  </a-space>
</template>
```

## 示例：自定义选择框展示内容

### 说明
通过 `#label` 插槽可以自定义选择框展示内容。




```vue
<template>
  <a-select default-value="Beijing" :style="{width:'320px'}" placeholder="Please select ...">
    <template #label="{ data }">
      <span><icon-plus/>{{data?.label}}</span>
    </template>
    <a-option>Beijing</a-option>
    <a-option>Shanghai</a-option>
    <a-option>Guangzhou</a-option>
    <a-option disabled>Disabled</a-option>
  </a-select>
</template>

<script>
import { IconPlus } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconPlus }
};
</script>
```

## 示例：联动选择框

### 说明
展示联动选择框的实现方法。




```vue

<template>
  <a-space>
    <a-select :style="{width:'200px'}" v-model="province">
      <a-option v-for="value of Object.keys(data)">{{value}}</a-option>
    </a-select>
    <a-select :style="{width:'200px'}" :options="data[province] || []" v-model="city" />
  </a-space>
</template>

<script>
import { ref, watch } from 'vue';

export default {
  setup() {
    const province = ref('Sichuan');
    const city = ref('Chengdu');
    const data = {
      Beijing: ['Haidian', 'Chaoyang', 'Changping'],
      Sichuan: ['Chengdu', 'Mianyang', 'Aba'],
      Guangdong: ['Guangzhou', 'Shenzhen', 'Shantou']
    };

    watch(province, () => {
      city.value = ''
    })

    return {
      province,
      city,
      data
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
  <a-select v-model="value" :options="options" :field-names="fieldNames" :style="{width:'320px'}"
            placeholder="Please select ..." />
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const value = ref('bj');
    const fieldNames = {value: 'city', label: 'text'}
    const options = reactive([
      {
        city: 'bj',
        text: 'Beijing'
      },
      {
        city: 'sh',
        text: 'Shanghai'
      },
      {
        city: 'gz',
        text: 'Guangzhou'
      },
      {
        city: 'cd',
        text: 'Chengdu'
      },
    ]);

    return {
      value,
      fieldNames,
      options
    }
  }
}
</script>
```

## 示例：虚拟列表

### 说明
虚拟列表的使用方法。




```vue

<template>
  <a-select :style="{width:'320px'}" :options="options" placeholder="Please select ..." :virtual-list-props="{height:200}" />
</template>

<script>
export default {
  setup() {
    const options = Array(1000).fill(null).map((_, index) => `Option ${index}`);

    return {
      options
    }
  },
}
</script>
```

## API


### `<select>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|multiple|是否开启多选模式（多选模式默认开启搜索）|`boolean`|`false`||
|model-value **(v-model)**|绑定值|`string\| number\| boolean\| Record<string, any>\| (string \| number \| boolean \| Record<string, any>)[]`|`-`||
|default-value|默认值（非受控模式）|`string\| number\| boolean\| Record<string, unknown>\| (string \| number \| boolean \| Record<string, unknown>)[]`|`'' \| []`||
|input-value **(v-model)**|输入框的值|`string`|`-`||
|default-input-value|输入框的默认值（非受控模式）|`string`|`''`||
|size|选择框的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|placeholder|占位符|`string`|`-`||
|loading|是否为加载中状态|`boolean`|`false`||
|disabled|是否禁用|`boolean`|`false`||
|error|是否为错误状态|`boolean`|`false`||
|allow-clear|是否允许清空|`boolean`|`false`||
|allow-search|是否允许搜索|`boolean \| { retainInputValue?: boolean }`|`false (single) \| true (multiple)`||
|allow-create|是否允许创建|`boolean`|`false`||
|max-tag-count|多选模式下，最多显示的标签数量。0 表示不限制|`number`|`0`||
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`-`||
|bordered|是否显示输入框的边框|`boolean`|`true`||
|default-active-first-option|是否在无值时默认选择第一个选项|`boolean`|`true`|2.43.0|
|popup-visible **(v-model)**|是否显示下拉菜单|`boolean`|`-`||
|default-popup-visible|弹出框默认是否可见（非受控模式）|`boolean`|`false`||
|unmount-on-close|是否在下拉菜单关闭时销毁元素|`boolean`|`false`||
|filter-option|是否过滤选项|`boolean \| ((inputValue: string, option: SelectOptionData) => boolean)`|`true`||
|options|选项数据|`(string \| number \| boolean \| SelectOptionData \| SelectOptionGroup)[]`|`[]`||
|virtual-list-props|传递虚拟列表属性，传入此参数以开启虚拟滚动 [VirtualListProps](#VirtualListProps)|`VirtualListProps`|`-`||
|trigger-props|下拉菜单的触发器属性|`TriggerProps`|`-`||
|format-label|格式化显示内容|`(data: SelectOptionData) => string`|`-`||
|fallback-option|自定义值中不存在的选项|`boolean\| ((    value: string \| number \| boolean \| Record<string, unknown>  ) => SelectOptionData)`|`true`|2.10.0|
|show-extra-options|是否在下拉菜单中显示额外选项|`boolean`|`true`|2.10.0|
|value-key|用于确定选项键值的属性名|`string`|`'value'`|2.18.0|
|search-delay|触发搜索事件的延迟时间|`number`|`500`|2.18.0|
|limit|多选时最多的选择个数|`number`|`0`|2.18.0|
|field-names|自定义 `SelectOptionData` 中的字段|`SelectFieldNames`|`-`|2.22.0|
|scrollbar|是否开启虚拟滚动条|`boolean \| ScrollbarProps`|`true`|2.38.0|
|show-header-on-empty|空状态时是否显示header|`boolean`|`false`||
|show-footer-on-empty|空状态时是否显示footer|`boolean`|`false`||
|tag-nowrap|标签内容不换行|`boolean`|`false`|2.56.1|
### `<select>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|change|值发生改变时触发|value: ` string \| number \| boolean \| Record<string, any> \| (string \| number \| boolean \| Record<string, any>)[] `||
|input-value-change|输入框的值发生改变时触发|inputValue: `string`||
|popup-visible-change|下拉框的显示状态改变时触发|visible: `boolean`||
|clear|点击清除按钮时触发|-||
|remove|点击标签的删除按钮时触发|removed: `string \| number \| boolean \| Record<string, any> \| undefined`||
|search|用户搜索时触发|inputValue: `string`||
|dropdown-scroll|下拉菜单发生滚动时触发|-||
|dropdown-reach-bottom|下拉菜单滚动到底部时触发|-||
|exceed-limit|多选超出限制时触发|value: `string \| number \| boolean \| Record<string, any> \| undefined`<br>ev: `Event`|2.18.0|
### `<select>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|trigger|自定义触发元素|-|2.22.0|
|prefix|前缀元素|-|2.22.0|
|search-icon|选择框的搜索图标|-|2.16.0|
|loading-icon|选择框的加载中图标|-|2.16.0|
|arrow-icon|选择框的箭头图标|-|2.16.0|
|footer|下拉框的页脚|-||
|header|下拉框的页头|-|2.43.0|
|label|选择框的显示内容|data: `SelectOptionData`||
|option|选项内容|data: `SelectOptionData`||
|empty|选项为空时的显示内容|-||




### `<option>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|value|选项值（如不填，会从内容中获取）|`string\|number\|boolean\|object`|`-`||
|label|选项标签（如不填，会从内容中获取）|`string`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|tag-props|展示的标签属性|`TagProps`|`-`|2.8.0|
|extra|额外数据。2.18.0 版本废弃，可使用对象形式的 value 扩展数据|`object`|`-`|2.10.0|
|index|用于手动指定选项的 index|`number`|`-`|2.20.0|




### `<optgroup>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|label|选项组的标题|`string`|`-`|
### `<optgroup>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|label|选项组的标题|-|2.10.0|



### Type

```ts
/**
 * @zh 选项
 * @en Option
 */
type Option = string | number | SelectOptionData | SelectOptionGroup;

/**
 * @zh 筛选
 * @en Filter
 */
type FilterOption = boolean | ((inputValue: string, option: SelectOptionData) => boolean);
```


### SelectOptionData

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|value|选项值|`string \| number \| boolean \| Record<string, unknown>`|`-`|
|label|选项内容|`string`|`-`|
|disabled|是否禁用|`boolean`|`false`|
|tagProps|选项对应的多选标签的属性|`any`|`-`|
|render|自定义渲染|`RenderFunction`|`-`|



### SelectOptionGroup

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|isGroup|是否为选项组|`true`|`-`|
|label|选项组标题|`string`|`-`|
|options|选项组中的选项|`SelectOption[]`|`-`|




### VirtualListProps

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|height|可视区域高度|`number \| string`|`-`||
|threshold|开启虚拟滚动的元素数量阈值，当数据数量小于阈值时不会开启虚拟滚动。|`number`|`-`||
|isStaticItemHeight|（已废除）元素高度是否是固定的。2.34.1 版本废除，请使用 `fixedSize`|`boolean`|`false`||
|fixedSize|元素高度是否是固定的。|`boolean`|`false`|2.34.1|
|estimatedSize|元素高度不固定时的预估高度。|`number`|`-`|2.34.1|
|buffer|视口边界外提前挂载的元素数量。|`number`|`10`|2.34.1|




## FAQ

### 使用 `Object` 格式作为选项的值
当使用 `Object` 格式作为选项的值时，需要通过 `value-key` 属性为选择器指定获取唯一标识的字段名，默认值为 `value`.
此外 `value` 的对象值需要在 `setup` 中定义好，不能够在模版中创建对象，这样会导致 `Option` 组件的重复渲染。

例如当我需要指定 `key` 为唯一标识时：
```vue
<template>
  <a-select v-model="value" :style="{width:'320px'}" placeholder="Please select ..." value-key="key">
    <a-option v-for="item of data" :value="item" :label="item.label" />
  </a-select>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const value = ref();
    const data = [{
      value: 'beijing',
      label: 'Beijing',
      key: 'extra1'
    }, {
      value: 'shanghai',
      label: 'Shanghai',
      key: 'extra2'
    }, {
      value: 'guangzhou',
      label: 'Guangzhou',
      key: 'extra3'
    }, {
      value: 'chengdu',
      label: 'Chengdu',
      key: 'extra4'
    }]

    return {
      value,
      data
    }
  },
}
</script>
```

### 滚动容器中的下拉菜单分离问题
`Select` 组件默认没有开启容器滚动的事件监听功能，如果遇到在滚动容器中下拉菜单分离的问题，可以手动开启内部 `Trigger` 组件的 `updateAtScroll` 功能。
如果是在全局环境中存在此种情况，可以使用 `ConfigProvider` 组件默认开启此属性。

```vue
<a-select :trigger-props="{updateAtScroll:true}"></a-select>
```
