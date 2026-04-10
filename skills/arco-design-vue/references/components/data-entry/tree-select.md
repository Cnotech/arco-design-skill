---
name: arco-vue-tree-select
description: "Arco Design Vue 树选择 TreeSelect 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-tree-select>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 树选择 TreeSelect

来源组件：上游 `web-vue/components/tree-select`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-tree-select>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
最简单的用法。




```vue
<template>
  <a-tree-select
    :data="treeData"
    placeholder="Please select ..."
    style="width: 300px"
  ></a-tree-select>
</template>
<script>
  import { h } from 'vue';
  import { IconCalendar } from '@arco-design/web-vue/es/icon';

  export default {
    setup() {
      return {
        treeData,
      };
    },
  };

  const treeData = [
    {
      key: 'node1',
      icon: () => h(IconCalendar),
      title: 'Trunk',
      disabled: true,
      children: [
        {
          key: 'node2',
          title: 'Leaf',
        },
      ],
    },
    {
      key: 'node3',
      title: 'Trunk2',
      icon: () => h(IconCalendar),
      children: [
        {
          key: 'node4',
          title: 'Leaf',
        },
        {
          key: 'node5',
          title: 'Leaf',
        },
      ],
    },
  ];
</script>
```

## 示例：设置 value 格式

### 说明
`labelInValue` 为 `true` 时，`value` 格式为： `{ label: string, value: string }`。




```vue
<template>
  <a-tree-select
    :data="treeData"
    :label-in-value="true"
    :default-value="{ value: 'node2', label: 'Leaf' }"
    placeholder="Please select ..."
    style="width: 300px"
    @change="onChange"
  ></a-tree-select>
</template>
<script>
  import { h } from 'vue';
  import { IconCalendar } from '@arco-design/web-vue/es/icon';

  export default {
    setup() {
      function onChange(value) {
        console.log(value);
      }

      return {
        onChange,
        treeData,
      };
    },
  };

  const treeData = [
    {
      key: 'node1',
      icon: () => h(IconCalendar),
      title: 'Trunk',
      disabled: true,
      children: [
        {
          key: 'node2',
          title: 'Leaf',
        },
      ],
    },
    {
      key: 'node3',
      title: 'Trunk2',
      icon: () => h(IconCalendar),
      children: [
        {
          key: 'node4',
          title: 'Leaf',
        },
        {
          key: 'node5',
          title: 'Leaf',
        },
      ],
    },
  ];
</script>
```

## 示例：双向绑定

### 说明
选中值支持双向绑定。




```vue
<template>
  <a-tree-select
    :data="treeData"
    v-model="selected"
    placeholder="Please select ..."
    style="width: 300px"
  ></a-tree-select>
</template>
<script>
  import { h, ref } from 'vue';
  import { IconCalendar } from '@arco-design/web-vue/es/icon';

  export default {
    setup() {
      const selected = ref('node2');

      return {
        selected,
        treeData,
      };
    },
  };

  const treeData = [
    {
      key: 'node1',
      icon: () => h(IconCalendar),
      title: 'Trunk',
      disabled: true,
      children: [
        {
          key: 'node2',
          title: 'Leaf',
        },
      ],
    },
    {
      key: 'node3',
      title: 'Trunk2',
      icon: () => h(IconCalendar),
      children: [
        {
          key: 'node4',
          title: 'Leaf',
        },
        {
          key: 'node5',
          title: 'Leaf',
        },
      ],
    },
  ];
</script>
```

## 示例：动态加载

### 说明
可以通过 `loadMore` 进行动态加载。此时可设置 `isLeaf` 来标示叶子节点。




```vue
<template>
  <a-tree-select
    :data="treeData"
    :load-more="loadMore"
    placeholder="Please select ..."
    style="width: 300px"
  ></a-tree-select>
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const treeData = ref(defaultTreeData);
      const loadMore = (nodeData) => {
        const { title, key } = nodeData;
        const children = [
          { title: `${title}-0`, value: `${title}-0`, key: `${key}-0` },
          { title: `${title}-1`, value: `${title}-1`, key: `${key}-1` },
        ];

        return new Promise((resolve) => {
          setTimeout(() => {
            nodeData.children = children;
            resolve();
          }, 1000);
        });
      };

      return {
        treeData,
        loadMore,
      };
    },
  };

  const defaultTreeData = [
    {
      key: 'node1',
      title: 'node1',
      disabled: true,
      children: [
        {
          key: 'node2',
          title: 'node2',
        },
      ],
    },
    {
      key: 'node3',
      title: 'node3',
      children: [
        {
          key: 'node4',
          title: 'node4',
          isLeaf: true,
        },
        {
          key: 'node5',
          title: 'node5',
          isLeaf: true,
        },
      ],
    },
  ];
</script>
```

## 示例：搜索

### 说明
设置 `:allow-search="true"` 启用搜索功能。动态加载时候只能在已加载数据中进行搜索。默认的关键字搜索是从`value`字段匹配。也可以传入 `filterTreeNode`自定义过滤方式。




```vue
<template>
  <a-space>
    <a-tree-select
      :allow-search="true"
      :allow-clear="true"
      :data="treeData"
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
    <a-tree-select
      :allow-search="true"
      :allow-clear="true"
      :data="treeData"
      :filter-tree-node="filterTreeNode"
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
  </a-space>
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      function filterTreeNode(searchValue, nodeData) {
        return nodeData.title.toLowerCase().indexOf(searchValue.toLowerCase()) > -1;
      }

      return {
        filterTreeNode,
        treeData,
      };
    },
  };

  const treeData = [
    {
      title: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Branch 0-0-1',
          key: '0-0-1',
          children: [
            {
              title: 'Leaf 0-0-1-1',
              key: '0-0-1-1'
            },
            {
              title: 'Leaf 0-0-1-2',
              key: '0-0-1-2'
            }
          ]
        },
      ],
    },
    {
      title: 'Trunk 0-1',
      key: '0-1',
      children: [
        {
          title: 'Branch 0-1-1',
          key: '0-1-1',
          children: [
            {
              title: 'Leaf 0-1-1-0',
              key: '0-1-1-0',
            }
          ]
        },
        {
          title: 'Branch 0-1-2',
          key: '0-1-2',
          children: [
            {
              title: 'Leaf 0-1-2-0',
              key: '0-1-2-0',
            }
          ]
        },
      ],
    },
  ];
</script>
```

## 示例：远程搜索

### 说明
监听 `search` 事件，在事件处理函数中获取数据并更新 `treeData`。 自定义搜索逻辑时，建议关闭内部过滤逻辑（`:disable-filter="true"`），以免影响自定义结果。




```vue
<template>
  <a-tree-select
    :allow-search="true"
    :allow-clear="true"
    :disable-filter="true"
    :data="treeData"
    :loading="loading"
    style="width: 300px"
    placeholder="Please select ..."
    @search="onSearch"
  ></a-tree-select>
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const treeData = ref(defaultTreeData);
      const loading = ref(false);

      function searchData(keyword) {
        const loop = (data) => {
          const result = [];
          data.forEach(item => {
            if (item.title.toLowerCase().indexOf(keyword.toLowerCase()) > -1) {
              result.push({...item});
            } else if (item.children) {
              const filterData = loop(item.children);
              if (filterData.length) {
                result.push({
                  ...item,
                  children: filterData
                })
              }
            }
          })
          return result;
        }

        return loop(defaultTreeData);
      }

      const onSearch = (searchKey) => {
        loading.value = true;
        setTimeout(() => {
          loading.value = false;
          treeData.value = searchData(searchKey);
        }, 200)
      };

      return {
        treeData,
        loading,
        onSearch,
      };
    },
  };

  const defaultTreeData = [
    {
      title: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Branch 0-0-1',
          key: '0-0-1',
          children: [
            {
              title: 'Leaf 0-0-1-1',
              key: '0-0-1-1'
            },
            {
              title: 'Leaf 0-0-1-2',
              key: '0-0-1-2'
            }
          ]
        },
      ],
    },
    {
      title: 'Trunk 0-1',
      key: '0-1',
      children: [
        {
          title: 'Branch 0-1-1',
          key: '0-1-1',
          children: [
            {
              title: 'Leaf 0-1-1-0',
              key: '0-1-1-0',
            }
          ]
        },
        {
          title: 'Branch 0-1-2',
          key: '0-1-2',
          children: [
            {
              title: 'Leaf 0-1-2-0',
              key: '0-1-2-0',
            }
          ]
        },
      ],
    },
  ];
</script>
```

## 示例：不同尺寸

### 说明
设置 `size` 可以使用四种尺寸（small, default, large, huge）的选择器。高度分别对应 24px、28px、32px、36px。




```vue
<template>
  <div style="margin-bottom: 20px;">
    <a-radio-group v-model="size" type='button'>
      <a-radio value="mini">mini</a-radio>
      <a-radio value="small">small</a-radio>
      <a-radio value="medium">medium</a-radio>
      <a-radio value="large">large</a-radio>
    </a-radio-group>
  </div>
  <a-tree-select
    defaultValue="node1"
    :size="size"
    :data="treeData"
    placeholder="Please select ..."
    style="width: 300px;"
  ></a-tree-select>
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const size = ref('medium');

      return {
        size,
        treeData,
      };
    },
  };

  const treeData = [
    {
      key: 'node1',
      title: 'node1',
      disabled: true,
      children: [
        {
          key: 'node2',
          title: 'node2',
        },
      ],
    },
    {
      key: 'node3',
      title: 'node3',
      children: [
        {
          key: 'node4',
          title: 'node4',
          isLeaf: true,
        },
        {
          key: 'node5',
          title: 'node5',
          isLeaf: true,
        },
      ],
    },
  ];
</script>
```

## 示例：下拉框的页头和页脚

### 说明
自定义树选择下拉框的页头和页脚




```vue
<template>
  <a-form layout="inline" :model="form">
   <a-form-item label="empty">
      <a-switch v-model="form.empty" />
    </a-form-item>
    <a-form-item label="showHeaderOnEmpty">
      <a-switch v-model="form.showHeaderOnEmpty" />
    </a-form-item>
    <a-form-item label="showFooterOnEmpty">
      <a-switch v-model="form.showFooterOnEmpty" />
    </a-form-item>
  </a-form>
  <a-tree-select
    style="width: 300px"
    placeholder="Please select ..."
    :data="computedTreeData"
    :show-header-on-empty="form.showHeaderOnEmpty"
    :show-footer-on-empty="form.showFooterOnEmpty"
  >
    <template #header>
      <div style="padding: 6px 12px;" >
        <a-checkbox value="1">All</a-checkbox>
      </div>
    </template>
      <template #footer>
      <div style="padding: 6px 0; text-align: center;">
        <a-button>Click Me</a-button>
      </div>
    </template>
  </a-tree-select>
</template>
<script>
  import { h, reactive, computed } from 'vue';
  import { IconCalendar } from '@arco-design/web-vue/es/icon';

  export default {
    setup() {
      const form = reactive({
        empty: false,
        showHeaderOnEmpty: false,
        showFooterOnEmpty: false,
      });

      const treeData = [
        {
          key: 'node1',
          icon: () => h(IconCalendar),
          title: 'Trunk',
          children: [
            {
              key: 'node2',
              title: 'Leaf',
            },
          ],
        },
        {
          key: 'node3',
          title: 'Trunk2',
          icon: () => h(IconCalendar),
          children: [
            {
              key: 'node4',
              title: 'Leaf',
            },
            {
              key: 'node5',
              title: 'Leaf',
            },
          ],
        },
        {
          key: 'node6',
          title: 'Trunk3',
          icon: () => h(IconCalendar),
          children: [
            {
              key: 'node7',
              title: 'Leaf',
            },
            {
              key: 'node8',
              title: 'Leaf',
            },
          ],
        },
      ];

      const computedTreeData = computed(() => {
        return form.empty ? [] : treeData;
      });

      return {
        form,
        computedTreeData,
      };
    },
  };
</script>
```

## 示例：自定义触发元素

### 说明
自定义触发元素。




```vue
<template>
  <a-tree-select
    :data="treeData"
    default-value="node1"
    @change="onChange"
  >
    <template #trigger>
      <a-typography-paragraph style="width: 300px">
        You selected: <a href='javascript: void(0)'>{{ text }}</a>
      </a-typography-paragraph>
    </template>
  </a-tree-select>
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const text = ref('node1');

      function onChange(selected) {
        text.value = selected;
      }

      return {
        treeData,
        text,
        onChange,
      };
    },
  };

  const treeData = [
    {
      key: 'node1',
      title: 'node1',
      children: [
        {
          key: 'node2',
          title: 'node2',
        },
      ],
    },
    {
      key: 'node3',
      title: 'node3',
      children: [
        {
          key: 'node4',
          title: 'node4',
        },
        {
          key: 'node5',
          title: 'node5',
          children: [
            {
              key: 'node6',
              title: 'node6',
            },
            {
              key: 'node7',
              title: 'node7',
            },
          ]
        },
      ],
    },
  ];
</script>
```

## 示例：多选

### 说明
多选




```vue
<template>
  <a-space>
    <a-tree-select
      v-model="selected"
      :multiple="true"
      :allow-clear="true"
      :allow-search="true"
      :data="treeData"
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
    <a-tree-select
      v-model="selected"
      :multiple="true"
      :max-tag-count="2"
      :allow-clear="true"
      :allow-search="true"
      :data="treeData"
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
  </a-space>
</template>
<script>
  import { h, ref } from 'vue';
  import { IconCalendar } from '@arco-design/web-vue/es/icon';

  export default {
    setup() {
      const selected = ref([]);

      return {
        selected,
        treeData,
      };
    },
  };

  const treeData = [
    {
      key: 'node1',
      icon: () => h(IconCalendar),
      title: 'node1',
      children: [
        {
          key: 'node2',
          title: 'node2',
        },
      ],
    },
    {
      key: 'node3',
      title: 'node3',
      icon: () => h(IconCalendar),
      children: [
        {
          key: 'node4',
          title: 'node4',
        },
        {
          key: 'node5',
          title: 'node5',
        },
      ],
    },
  ];
</script>
```

## 示例：复选框多选

### 说明
可以通过设置 `treeCheckable` 属性开启复选框勾选。




```vue
<template>
  <div style="marginBottom: 24px;">
    <a-checkbox
      v-model="treeCheckStrictly"
      @change="() => {
        selected = [];
      }"
    >
    treeCheckStrictly
    </a-checkbox>
  </div>
  <a-tree-select
    v-model="selected"
    :allow-search="true"
    :allow-clear="true"
    :tree-checkable="true"
    :tree-check-strictly="treeCheckStrictly"
    :data="treeData"
    placeholder="Please select ..."
    style="width: 300px;"
  ></a-tree-select>
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const selected = ref([]);
      const treeCheckStrictly = ref(false);

      return {
        selected,
        treeCheckStrictly,
        treeData,
      };
    },
  };

  const treeData = [
    {
      title: 'Trunk 0-0',
      value: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Leaf 0-0-1',
          value: 'Leaf 0-0-1',
          key: '0-0-1',
        },
        {
          title: 'Branch 0-0-2',
          value: 'Branch 0-0-2',
          key: '0-0-2',
          children: [
            {
              title: 'Leaf 0-0-2-1',
              value: 'Leaf 0-0-2-1',
              key: '0-0-2-1'
            }
          ]
        },
      ],
    },
    {
      title: 'Trunk 0-1',
      value: 'Trunk 0-1',
      key: '0-1',
      children: [
        {
          title: 'Branch 0-1-1',
          value: 'Branch 0-1-1',
          key: '0-1-1',
          checkable: false,
          children: [
            {
              title: 'Leaf 0-1-1-1',
              value: 'Leaf 0-1-1-1',
              key: '0-1-1-1',
            },
            {
              title: 'Leaf 0-1-1-2',
              value: 'Leaf 0-1-1-2',
              key: '0-1-1-2',
              disabled: true
            },
          ]
        },
        {
          title: 'Leaf 0-1-2',
          value: 'Leaf 0-1-2',
          key: '0-1-2',
        },
      ],
    },
  ];
</script>
```

## 示例：定制回填方式

### 说明
可以通过`treeCheckStrategy`属性定制回填方式。




```vue
<template>
  <div style="margin-bottom: 24px;">
    <a-radio-group
      type='button'
      v-model="treeCheckedStrategy"
      @change="(value) => {
        selected = []
      }"
    >
      <a-radio
        v-for="item in strategyOptions"
        :key="item?.value"
        :value="item?.value"
      >
        {{ item?.label }}
      </a-radio>
    </a-radio-group>
  </div>
  <a-tree-select
    v-model="selected"
    :allow-search="true"
    :allow-clear="true"
    :tree-checkable="true"
    :tree-checked-strategy="treeCheckedStrategy"
    :data="treeData"
    placeholder="Please select ..."
    style="width: 300px;"
  ></a-tree-select>
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const selected = ref([]);
      const treeCheckedStrategy = ref('all');

      return {
        selected,
        treeCheckedStrategy,
        strategyOptions,
        treeData,
      };
    },
  };

  const strategyOptions = [
    {
      value: 'all',
      label: 'show all'
    },
    {
      value: 'parent',
      label: 'show parent'
    },
    {
      value: 'child',
      label: 'show child'
    }
  ];

  const treeData = [
    {
      title: 'Trunk 0-0',
      value: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Leaf 0-0-1',
          value: 'Leaf 0-0-1',
          key: '0-0-1',
        },
        {
          title: 'Branch 0-0-2',
          value: 'Branch 0-0-2',
          key: '0-0-2',
          children: [
            {
              title: 'Leaf 0-0-2-1',
              value: 'Leaf 0-0-2-1',
              key: '0-0-2-1'
            }
          ]
        },
      ],
    },
    {
      title: 'Trunk 0-1',
      value: 'Trunk 0-1',
      key: '0-1',
      children: [
        {
          title: 'Branch 0-1-1',
          value: 'Branch 0-1-1',
          key: '0-1-1',
          checkable: false,
          children: [
            {
              title: 'Leaf 0-1-1-1',
              value: 'Leaf 0-1-1-1',
              key: '0-1-1-1',
            },
            {
              title: 'Leaf 0-1-1-2',
              value: 'Leaf 0-1-1-2',
              key: '0-1-1-2',
              disabled: true
            },
          ]
        },
        {
          title: 'Leaf 0-1-2',
          value: 'Leaf 0-1-2',
          key: '0-1-2',
        },
      ],
    },
  ];
</script>
```

## 示例：控制下拉框的展开收起

### 说明
通过 `popupVisible` (支持 `v-model`) 控制下拉框的展开和收起。




```vue
<template>
  <div style="margin-bottom: 24px;">
    <a-button type="primary" @click="onClick">toggle</a-button>
  </div>
  <a-tree-select
    :popupVisible="popupVisible"
    :allow-clear="true"
    :data="treeData"
    placeholder="Please select ..."
    style="width: 300px"
  ></a-tree-select>
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const popupVisible = ref(false);
      function onClick() {
        popupVisible.value = !popupVisible.value;
      }

      return {
        onClick,
        popupVisible,
        treeData,
      };
    },
  };

  const treeData = [
    {
      key: 'node1',
      title: 'Trunk',
      children: [
        {
          key: 'node2',
          title: 'Leaf',
        },
      ],
    },
    {
      key: 'node3',
      title: 'Trunk2',
      children: [
        {
          key: 'node4',
          title: 'Leaf',
        },
        {
          key: 'node5',
          title: 'Leaf',
        },
      ],
    },
  ];
</script>
```

## 示例：自定义 TreeData 的字段名称

### 说明
通过 `fieldNames` 字段可以自定义 TreeData 的字段名。




```vue
<template>
  <a-tree-select
    default-value="0-0-1"
    :fieldNames="{
      key: 'value',
      title: 'label',
      children: 'items'
    }"
    :data="treeData"
    placeholder="Please select ..."
    style="width: 300px;"
  ></a-tree-select>
</template>
<script>
  export default {
    setup() {
      return {
        treeData,
      };
    },
  };

  const treeData = [
    {
      label: 'Trunk 0-0',
      value: '0-0',
      items: [
        {
          label: 'Branch 0-0-2',
          value: '0-0-2',
          selectable: false,
          items: [
            {
              label: 'Leaf',
              value: '0-0-2-1',
              items: [
                {
                  label: 'Leaf 0-0-2',
                  value: '0-0-2-1-0',
                  items: [
                    {
                      label: 'Leaf',
                      value: '0-0-2-1-0-0'
                    }
                  ]
                },
              ],
            }
          ]
        },
      ],
    },
    {
      label: 'Trunk 0-1',
      value: '0-1',
      items: [
        {
          label: 'Branch 0-1-1',
          value: '0-1-1',
          items: [
            {
              label: 'Leaf',
              value: '0-1-1-0',
            }
          ]
        },
      ],
    },
  ];
</script>
```

## 示例：虚拟列表

### 说明
通过指定 `treeProps.virtualListProps` 来开启虚拟列表，在大量数据时获得高性能表现。



```vue
<template>
  <a-tree-select
    :data="treeData"
    :allow-search="{
      retainInputValue: true
    }"
    multiple
    tree-checkable
    :scrollbar="false"
    tree-checked-strategy="parent"
    :treeProps="{
      virtualListProps: {
        height: 200,
      },
    }"
  />
</template>
<script>
export default {
  setup() {
    const treeData = loop();
    return {
      treeData
    }
  }
}

function loop(path = '0', level = 2) {
  const list = [];
  for (let i = 0; i < 10; i += 1) {
    const key = `${path}-${i}`;
    const treeNode = {
      title: key,
      key,
    };

    if (level > 0) {
      treeNode.children = loop(key, level - 1);
    }

    list.push(treeNode);
  }
  return list;
}
</script>
```

## 示例：回退选项

### 说明
使用 `fallback-option` 自定义找不到选项的值的显示效果，默认找不到选项就展示值本身。用户可以将其设定为 `false` 来隐藏那些没有匹配到节点数据的值。




```vue

<template>
  <a-space direction="vertical" size="large">
    <a-tree-select
      defaultValue="node0"
      :data="treeData"
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
    <a-tree-select
      defaultValue="node0"
      :data="treeData"
      :fallback-option="false"
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
    <a-tree-select
      defaultValue="node0"
      :data="treeData"
      :fallback-option="fallback"
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
    <a-tree-select
      :defaultValue="['node0', 'node2']"
      :data="treeData"
      multiple
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
    <a-tree-select
      :defaultValue="['node0', 'node2']"
      :data="treeData"
      :fallback-option="false"
      multiple
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
    <a-tree-select
      :default-value="['node0', 'node2']"
      :data="treeData"
      :fallback-option="fallback"
      multiple
      placeholder="Please select ..."
      style="width: 300px"
    ></a-tree-select>
  </a-space>
</template>

<script>
export default {
  setup() {
    return {
      treeData,
      fallback(key) {
        return {
          key,
          title: `++${key}++`
        }
      }
    }
  }
}

const treeData = [
    {
      key: 'node1',
      title: 'Trunk1',
      children: [
        {
          key: 'node2',
          title: 'Leaf1',
        },
      ],
    },
    {
      key: 'node3',
      title: 'Trunk2',
      children: [
        {
          key: 'node4',
          title: 'Leaf2',
        },
        {
          key: 'node5',
          title: 'Leaf3',
        },
      ],
    },
  ];
</script>
```

## API


### `<tree-select>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|disabled|是否禁用|`boolean`|`false`||
|loading|是否为加载中状态|`boolean`|`false`||
|error|是否为错误状态|`boolean`|`false`||
|size|选择框的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|border|是否显示边框|`boolean`|`true`||
|allow-search|是否允许搜索|`boolean \| { retainInputValue?: boolean }`|`false (single) \| true (multiple)`||
|allow-clear|是否允许清除|`boolean`|`false`||
|placeholder|提示文案|`string`|`-`||
|max-tag-count|最多显示的标签数量，仅在多选模式有效|`number`|`-`||
|multiple|是否支持多选|`boolean`|`false`||
|default-value|默认值|`string \| number \| Array<string \| number> \| LabelValue \| LabelValue[]`|`-`||
|model-value **(v-model)**|绑定值|`string \| number \| Array<string \| number> \| LabelValue \| LabelValue[]`|`-`||
|field-names|指定节点数据中的字段名|`TreeFieldNames`|`-`||
|data|数据|`TreeNodeData[]`|`[]`||
|label-in-value|设置value格式。默认是string，设置为true时候，value格式为： { label: string, value: string }|`boolean`|`false`||
|tree-checkable|是否展示复选框|`boolean`|`false`||
|tree-check-strictly|父子节点是否关联|`boolean`|`false`||
|tree-checked-strategy|定制回显方式|`'all' \| 'parent' \| 'child'`|`'all'`||
|tree-props|可以接受所有 [Tree](/vue/component/tree) 组件的Props|`Partial<TreeProps>`|`-`||
|trigger-props|可以接受所有 [Trigger](/vue/component/trigger) 组件的Props|`Partial<TriggerProps>`|`-`||
|popup-visible **(v-model)**|弹出框是否可见|`boolean`|`-`||
|default-popup-visible|默认弹出框是否可见|`boolean`|`false`||
|dropdown-style|下拉框样式|`CSSProperties`|`-`||
|dropdown-class-name|下拉框样式 class|`string \| string[]`|`-`||
|filter-tree-node|自定义节点过滤函数|`(searchKey: string, nodeData: TreeNodeData) => boolean`|`-`||
|load-more|动态加载数据|`(nodeData: TreeNodeData) => Promise<void>`|`-`||
|disable-filter|禁用内部过滤逻辑|`boolean`|`false`||
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`-`||
|fallback-option|为 value 中找不到匹配项的 key 定义节点数据|`boolean \| ((key: number \| string) => TreeNodeData \| boolean)`|`true`|2.22.0|
|selectable|设置可选择的节点，默认全部可选|`boolean\| 'leaf'\| ((    node: TreeNodeData,    info: { isLeaf: boolean; level: number }  ) => boolean)`|`true`|2.27.0|
|scrollbar|是否开启虚拟滚动条|`boolean \| ScrollbarProps`|`true`|2.39.0|
|show-header-on-empty|空状态时是否显示header|`boolean`|`false`||
|show-footer-on-empty|空状态时是否显示footer|`boolean`|`false`||
|input-value **(v-model)**|输入框的值|`string`|`-`|2.55.0|
|default-input-value|输入框的默认值（非受控模式）|`string`|`''`|2.55.0|
### `<tree-select>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|change|值改变时触发|value: `string \| number \| LabelValue \| Array<string \| number> \| LabelValue[] \| undefined`||
|popup-visible-change|下拉框显示状态改变时触发|visible: `boolean`||
|search|搜索值变化时触发|searchKey: `string`||
|clear|点击清除时触发|-||
|input-value-change|输入框的值发生改变时触发|inputValue: `string`|2.55.0|
### `<tree-select>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|trigger|自定义触发元素|-||
|prefix|前缀|-||
|label|自定义选择框显示|data: `mixed`||
|header|自定义下拉框页头|-||
|loader|定制加载中显示的内容|-||
|empty|定制空数据展示|-||
|footer|自定义下拉框页脚|-||
|tree-slot-extra|定制 tree 组件的渲染额外节点内容|-||
|tree-slot-title|定制 tree 组件的节点标题|title: `string`||
|tree-slot-icon|定制 tree 组件的节点图标|node: `TreeNodeData`|2.18.0|
|tree-slot-switcher-icon|定制 tree 组件的 switcher 图标|-||
