---
name: arco-vue-table
description: "Arco Design Vue 表格 Table 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-table>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 表格 Table

来源组件：上游 `web-vue/components/table`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-table>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
表格的基本用法，需要传递 `columns` 和 `data`。




```vue
<template>
  <a-table :columns="columns" :data="data" />
</template>

<script>
import { reactive } from 'vue';

export default {
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
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    return {
      columns,
      data
    }
  },
}
</script>
```

## 示例：行选择器

### 说明
通过设置 `row-selection` 开启行选择器。




```vue
<template>
  <a-space direction="vertical" size="large" fill>
    <div>
      <span>OnlyCurrent: </span>
      <a-switch v-model="rowSelection.onlyCurrent" />
    </div>
    <a-table row-key="name" :columns="columns" :data="data" :row-selection="rowSelection"
             v-model:selectedKeys="selectedKeys" :pagination="pagination" />
  </a-space>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const selectedKeys = ref(['Jane Doe', 'Alisa Ross']);

    const rowSelection = reactive({
      type: 'checkbox',
      showCheckedAll: true,
      onlyCurrent: false,
    });
    const pagination = {pageSize: 5}

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
    ]
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com',
      disabled: true
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }, {
      key: '6',
      name: 'Jane Doe 2',
      salary: 15000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '7',
      name: 'Alisa Ross 2',
      salary: 28000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '8',
      name: 'Kevin Sandra 2',
      salary: 26000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com',
    }, {
      key: '9',
      name: 'Ed Hellen 2',
      salary: 18000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '10',
      name: 'William Smith 2',
      salary: 12000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    return {
      rowSelection,
      columns,
      data,
      selectedKeys,
      pagination
    }
  },
}
</script>
```

## 示例：行选择器（单选框）

### 说明
通过设置 `rowSelection.type='radio'` 开启单选模式。




```vue
<template>
  <a-table :columns="columns" :data="data" :row-selection="rowSelection" />
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const rowSelection = {
      type: 'radio'
    };
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
    ]
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    return {
      rowSelection,
      columns,
      data
    }
  },
}
</script>
```

## 示例：展开行

### 说明
通过设置 `expandable` 开启展开行功能。可以在 `data` 中添加 `expand` 属性，设置展开行显示内容。




```vue
<template>
  <a-table :columns="columns" :data="data" :expandable="expandable" />
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const expandable = reactive({
      title: 'Expand',
      width: 80,
      expandedRowRender: (record) => {
        if(record.key==='3'){
          return `My Name is ${record.name}`
        }
      }
    });

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

    const data = reactive([
      {
        key: '1',
        name: 'Jane Doe',
        salary: 23000,
        address: '32 Park Road, London',
        email: 'jane.doe@example.com',
        expand: 'Expand Data'
      }, {
        key: '2',
        name: 'Alisa Ross',
        salary: 25000,
        address: '35 Park Road, London',
        email: 'alisa.ross@example.com'
      }, {
        key: '3',
        name: 'Kevin Sandra',
        salary: 22000,
        address: '31 Park Road, London',
        email: 'kevin.sandra@example.com'
      }, {
        key: '4',
        name: 'Ed Hellen',
        salary: 17000,
        address: '42 Park Road, London',
        email: 'ed.hellen@example.com'
      }, {
        key: '5',
        name: 'William Smith',
        salary: 27000,
        address: '62 Park Road, London',
        email: 'william.smith@example.com'
      }
    ]);

    return {
      columns,
      expandable,
      data
    }
  },
}
</script>
```

## 示例：文本省略和提示

### 说明
开启 `ellipsis` 属性可以显示省略号，如果同时开启 `tooltip` 会在显示省略号时使用文本提示。注意：开启 `tooltip` 后会修改 `table-cell` 中的 DOM 结构。




```vue
<template>
  <a-table :columns="columns" :data="data" />
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
        ellipsis: true,
        tooltip: true,
        width: 100
      },
      {
        title: 'Salary',
        dataIndex: 'salary',
      },
      {
        title: 'Address',
        dataIndex: 'address',
        ellipsis: true,
        width: 150,
      },
      {
        title: 'Email',
        dataIndex: 'email',
        ellipsis: true,
        tooltip: {position: 'left'},
        width: 200,
      },
    ];
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    return {
      columns,
      data
    }
  },
}
</script>
```

## 示例：树形数据展示

### 说明
树形数据展示的例子，`data` 里有 `children` 字段时会展示为树形表格。




```vue

<template>
  <a-space>
    <span>checkStrictly:</span>
    <a-switch v-model="rowSelection.checkStrictly" />
  </a-space>
  <a-table :columns="columns" :data="data" v-model:expandedKeys="expandedKeys" :row-selection="rowSelection" show-empty-tree style="margin-top: 20px"/>
</template>

<script>
import { ref,reactive } from 'vue';

export default {
  setup() {
    const expandedKeys = ref([]);


    const rowSelection = reactive({
      type: 'checkbox',
      showCheckedAll: true,
      checkStrictly: true
    });

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
    const data = [{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com',
      children: [
        {
          key: '2',
          name: 'Alisa Ross',
          salary: 25000,
          address: '35 Park Road, London',
          email: 'alisa.ross@example.com',
          children: [
            {
              key: '3',
              name: 'Ed Hellen',
              salary: 17000,
              address: '42 Park Road, London',
              email: 'ed.hellen@example.com'
            }, {
              key: '4',
              name: 'William Smith',
              salary: 27000,
              address: '62 Park Road, London',
              email: 'william.smith@example.com'
            }
          ]
        },
        {
          key: '5',
          name: 'Alisa Ross',
          salary: 25000,
          address: '35 Park Road, London',
          email: 'alisa.ross@example.com'
        }
      ]
    }, {
      key: '6',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '7',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '8',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '9',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com',
      children:[]
    }];

    return {
      columns,
      data,
      expandedKeys,
      rowSelection
    }
  },
}
</script>
```

## 示例：子树懒加载

### 说明
通过 `load-more` 属性可以开启子树懒加载功能。
开启子树懒加载功能后，需要在无子树节点标注 `isLeaf: true`，没有标注且没有 `children` 属性的节点会认为需要子树懒加载处理。
`load-more` 属性有提供 `done` 函数进行回调，可以在回调中传入懒加载的子树。如果 `done` 函数没有传入数据会认为懒加载失败，此节点可以再次触发懒加载。




```vue

<template>
  <a-table :columns="columns" :data="data" :load-more="loadMore" />
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const columns = [{
      title: 'Name',
      dataIndex: 'name',
    }, {
      title: 'Salary',
      dataIndex: 'salary',
    }, {
      title: 'Address',
      dataIndex: 'address',
    }, {
      title: 'Email',
      dataIndex: 'email',
    }];
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com',
      children: [{
        key: '2',
        name: 'Alisa Ross',
        salary: 25000,
        address: '35 Park Road, London',
        email: 'alisa.ross@example.com',
      }, {
        key: '5',
        name: 'Alisa Ross',
        salary: 25000,
        address: '35 Park Road, London',
        email: 'alisa.ross@example.com',
        isLeaf: true,
      }]
    }, {
      key: '6',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com',
    }, {
      key: '7',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com',
      isLeaf: true,
    }, {
      key: '8',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com',
      isLeaf: true,
    }, {
      key: '9',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com',
      isLeaf: true,
    }])

    const loadMore = (record, done) => {
      window.setTimeout(() => {
        done([
          {
            key: `${record.key}-1`,
            name: 'Ed Hellen',
            salary: 17000,
            address: '42 Park Road, London',
            email: 'ed.hellen@example.com',
            isLeaf: true,
          }, {
            key: `${record.key}-2`,
            name: 'William Smith',
            salary: 27000,
            address: '62 Park Road, London',
            email: 'william.smith@example.com',
            isLeaf: true,
          }
        ])
      }, 2000)
    }

    return {
      columns,
      data,
      loadMore
    }
  },
}
</script>
```

## 示例：表格属性

### 说明
这里罗列了一些表格的属性，你可以方便的打开或关闭一些属性，查看它的效果。




```vue

<template>
  <a-form layout="inline" :model="form">
    <a-form-item label="Border" field="border">
      <a-switch v-model="form.border" />
    </a-form-item>
    <a-form-item label="Hover" field="hover">
      <a-switch v-model="form.hover" />
    </a-form-item>
    <a-form-item label="stripe" field="stripe">
      <a-switch v-model="form.stripe" />
    </a-form-item>
    <a-form-item label="checkbox" field="checkbox">
      <a-switch v-model="form.checkbox" />
    </a-form-item>
    <a-form-item label="checkAll" field="checkAll">
      <a-switch v-model="rowSelection.showCheckedAll" />
    </a-form-item>
    <a-form-item label="loading" field="loading">
      <a-switch v-model="form.loading" />
    </a-form-item>
    <a-form-item label="tableHeader" field="tableHeader">
      <a-switch v-model="form.tableHeader" />
    </a-form-item>
    <a-form-item label="noData" field="noData">
      <a-switch v-model="form.noData" />
    </a-form-item>
  </a-form>
  <a-table
    :columns="columns"
    :data="form.noData ? [] : data"
    :bordered="form.border"
    :hoverable="form.hover"
    :stripe="form.stripe"
    :loading="form.loading"
    :show-header="form.tableHeader"
    :row-selection="form.checkbox ? rowSelection : undefined"
  />
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      border: true,
      borderCell: false,
      hover: true,
      stripe: false,
      checkbox: true,
      loading: false,
      tableHeader: true,
      noData: false
    });

    const rowSelection = reactive({
      type: 'checkbox',
      showCheckedAll: true
    });

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

    const data = [{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }];

    return {
      form,
      rowSelection,
      columns,
      data
    }
  },
}
</script>
```

## 示例：排序和筛选

### 说明
通过设置 `columns` 中的 `sortable` 和 `filterable` 属性，可以配置排序和筛选功能。 通过 `filter-icon-align-left` 属性可以让筛选按钮左对齐。
可以通过设置 `sortable.sorter=true` 来关闭内部排序，并通过 `change` 或者 `sorterChange` 事件来实现服务器端排序。




```vue
<template>
  <a-space direction="vertical" size="large" fill>
    <a-space>
      <a-switch v-model="alignLeft" />
      <span>Filter icon align left: {{alignLeft}}</span>
    </a-space>
    <a-table :columns="columns" :data="data" :filter-icon-align-left="alignLeft" @change="handleChange" />
  </a-space>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const alignLeft = ref(false);

    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
        sortable: {
          sortDirections: ['ascend', 'descend']
        }
      },
      {
        title: 'Salary',
        dataIndex: 'salary',
        sortable: {
          sortDirections: ['ascend']
        },
        filterable: {
          filters: [{
            text: '> 20000',
            value: '20000',
          }, {
            text: '> 30000',
            value: '30000',
          }],
          filter: (value, record) => record.salary > value,
          multiple: true
        }
      },
      {
        title: 'Address',
        dataIndex: 'address',
        filterable: {
          filters: [{
            text: 'London',
            value: 'London',
          }, {
            text: 'Paris',
            value: 'Paris',
          },],
          filter: (value, row) => row.address.includes(value),
        }
      },
      {
        title: 'Email',
        dataIndex: 'email',
      },
    ];
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    const handleChange = (data, extra, currentDataSource) => {
      console.log('change', data, extra, currentDataSource)
    }

    return {
      alignLeft,
      columns,
      data,
      handleChange
    }
  },
}
</script>
```

## 示例：自定义筛选菜单

### 说明
通过插槽可以自定义筛选菜单内容。




```vue

<template>
  <a-table :columns="columns" :data="data" @change="handleChange">
    <template #name-filter="{ filterValue, setFilterValue, handleFilterConfirm, handleFilterReset}">
      <div class="custom-filter">
        <a-space direction="vertical">
          <a-input :model-value="filterValue[0]" @input="(value)=>setFilterValue([value])" />
          <div class="custom-filter-footer">
            <a-button @click="handleFilterConfirm">Confirm</a-button>
            <a-button @click="handleFilterReset">Reset</a-button>
          </div>
        </a-space>
      </div>
    </template>
  </a-table>
</template>

<script>
import { reactive, h } from 'vue';
import { IconSearch } from '@arco-design/web-vue/es/icon';

export default {
  setup() {
    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
        filterable: {
          filter: (value, record) => record.name.includes(value),
          slotName: 'name-filter',
          icon: () => h(IconSearch)
        }
      },
      {
        title: 'Salary',
        dataIndex: 'salary',
        sortable: {
          sortDirections: ['ascend']
        },
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
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    const handleChange = (data, extra, currentDataSource) => {
      console.log('change', data, extra, currentDataSource)
    }

    return {
      columns,
      data,
      handleChange
    }
  },
}
</script>

<style>
.custom-filter {
  padding: 20px;
  background: var(--color-bg-5);
  border: 1px solid var(--color-neutral-3);
  border-radius: var(--border-radius-medium);
  box-shadow: 0 2px 5px rgb(0 0 0 / 10%);
}

.custom-filter-footer {
  display: flex;
  justify-content: space-between;
}
</style>
```

## 示例：表格滚动

### 说明
设置 scroll 属性可以开启表格滚动。x 指表格的实际宽度，一般设置的值会大于表格容器宽度；y 指表格的显示高度，表格实际高度超出后会显示滚动条。
2.18.0 版本后 x, y 均可设置百分比。y 设置为 100% 可以让表格容器高度跟随外层容器，超出后自动显示滚动条。




```vue
<template>
  <div style="margin-bottom: 20px">
    <a-switch v-model="scrollbar" />
    Virtual Scrollbar
  </div>
  <a-table :columns="columns" :data="data" :scroll="scroll" :scrollbar="scrollbar" />
  <a-split direction="vertical" :default-size="0.9" :style="{height: '500px', marginTop: '30px'}">
    <template #first>
      <a-table :columns="columns" :data="data" :scroll="scrollPercent" :scrollbar="scrollbar" />
    </template>
  </a-split>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const scrollbar = ref(true);
    const scroll = {
      x: 2000,
      y: 200
    };
    const scrollPercent = {
      x: '120%',
      y: '100%'
    };
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
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    return {
      scroll,
      scrollPercent,
      columns,
      data,
      scrollbar
    }
  },
}
</script>
```

## 示例：固定列

### 说明
在 `columns` 中指定 `fixed: 'left'` 或 `fixed: 'right'`，可将列固定到左侧或右侧。设置了 `fixed` 的列必须设置 `width` 指定列的宽度。
**注意**：要配合 `:scroll="{ x: number }"` 使用。此外 `columns` 中至少需要有一列不设置宽度，自适应，不然会有样式问题。





```vue
<template>
  <a-table :columns="columns" :data="data" :scroll="scroll" :expandable="expandable" />
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
        fixed: 'left',
        width: 140
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
        fixed: 'right',
        width: 200
      },
    ];

    const expandable = {
      title: 'Expand',
      width: 80,
    }

    const scroll = {
      x: 2000,
      y: 200
    }

    const data = reactive([
      {
        key: '1',
        name: 'Jane Doe',
        salary: 23000,
        address: '32 Park Road, London',
        email: 'jane.doe@example.com',
        expand: 'Expand Content'
      }, {
        key: '2',
        name: 'Alisa Ross',
        salary: 25000,
        address: '35 Park Road, London',
        email: 'alisa.ross@example.com'
      }, {
        key: '3',
        name: 'Kevin Sandra',
        salary: 22000,
        address: '31 Park Road, London',
        email: 'kevin.sandra@example.com'
      }, {
        key: '4',
        name: 'Ed Hellen',
        salary: 17000,
        address: '42 Park Road, London',
        email: 'ed.hellen@example.com'
      }, {
        key: '5',
        name: 'William Smith',
        salary: 27000,
        address: '62 Park Road, London',
        email: 'william.smith@example.com'
      }
    ]);

    return {
      columns,
      expandable,
      scroll,
      data
    }
  },
}
</script>
```

## 示例：单元格合并

### 说明
通过 `span-method` 属性进行单元格合并。可以设置 `span-all` 让列索引包含操作列，注意：目前如果合并多项选择器会导致全选状态判断错误。




```vue
<template>
  <a-space direction="vertical" size="large" style="width: 100%">
    <a-table :columns="columns" :data="data" :span-method="spanMethod" />
    <a-table :columns="columns" :data="data" :span-method="dataSpanMethod" :bordered="{wrapper: true, cell: true}" />
    <a-table :columns="columns" :data="data" :row-selection="{type: 'checkbox'}" :span-method="spanMethodAll" span-all :bordered="{wrapper: true, cell: true}" />
  </a-space>
</template>

<script>
export default {
  setup(){
    const spanMethod= ({rowIndex, columnIndex}) => {
      if (rowIndex === 1 && columnIndex === 1) {
        return {
          rowspan: 2,
          colspan: 3
        }
      }
    };
    const  dataSpanMethod= ({record, column}) => {
      if (record.name === 'Alisa Ross' && column.dataIndex === 'salary') {
        return {
          rowspan: 2,
        }
      }
    };
    const  spanMethodAll= ({rowIndex, columnIndex}) => {
      if (rowIndex === 1 && columnIndex === 0) {
        return {rowspan: 2}
      }

      if (rowIndex === 1 && columnIndex === 2) {
        return {
          rowspan: 2,
          colspan: 3
        }
      }
    };
    const columns=[
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
    const data=[{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }];

    return {
      spanMethod,
      dataSpanMethod,
      spanMethodAll,
      columns,
      data
    }
  },
}
</script>
```

## 示例：表头吸顶

### 说明
通过 `sticky-header` 设置表头吸顶。表头吸顶的计算容器为最近滚动容器，设置数字时可指定距离滚动容器顶部的高度。




```vue
<template>
  <a-table :columns="columns" :data="data" :sticky-header="60"/>
</template>

<script>
import { reactive } from 'vue';

export default {
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
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    return {
      columns,
      data
    }
  },
}
</script>
```

## 示例：总结行

### 说明
设置 `summary` 可以开启表尾总结行，并可以通过 `summary-text` 指定首列文字。
如果想要自定义总结行展示，可以传入函数。函数的返回值为需要展示的数据，结构同 `data` 一样即可，支持多行数据。
注意：控制列暂不可以自定义内容




```vue

<template>
  <a-table :columns="columns" :data="data" :summary="true" :summary-span-method="spanMethod" />
  <a-table :columns="columns" :data="data" :scroll="scroll" :expandable="expandable" :summary="summary">
    <template #summary-cell="{ column,record,rowIndex }">
      <div :style="getColorStyle(column,record)">{{record[column.dataIndex]}}</div>
    </template>
  </a-table>
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const expandable = {
      title: 'Expand',
      width: 80
    };
    const scroll = {
      x: 2000,
      y: 200
    }
    const columns = reactive([
      {
        title: 'Name',
        dataIndex: 'name',
        fixed: 'left',
        width: 140
      },
      {
        title: 'Salary',
        dataIndex: 'salary',
        summaryCellStyle: (record) => {
          if (record.salary > 100000) {
            return {
              backgroundColor: 'rgb(var(--arcoblue-6))',
              color: '#fff'
            }
          }
        }
      },
      {
        title: 'Data1',
        dataIndex: 'data1',
      },
      {
        title: 'Data2',
        dataIndex: 'data2',
      },
    ]);
    const data = reactive([
      {
        key: '1',
        name: 'Jane Doe',
        salary: 23000,
        data1: 10,
        data2: 8,
        expand: 'Expand Content'
      }, {
        key: '2',
        name: 'Alisa Ross',
        salary: 25000,
        data1: 9,
        data2: -12,
      }, {
        key: '3',
        name: 'Kevin Sandra',
        salary: 22000,
        data1: 15,
        data2: -2,
      }, {
        key: '4',
        name: 'Ed Hellen',
        salary: 17000,
        data1: 2,
        data2: 3,
      }, {
        key: '5',
        name: 'William Smith',
        salary: 27000,
        data1: 11,
        data2: 0,
      }
    ])

    const summary = ({columns, data}) => {
      let countData = {
        salary: 0,
        data1: 0,
        data2: 0
      };
      data.forEach(record => {
        countData.salary += record.salary;
        countData.data1 += record.data1;
        countData.data2 += record.data2;
      })


      return [{
        name: 'Avg',
        salary: countData.salary / data.length,
        data1: countData.data1 / data.length,
        data2: countData.data2 / data.length,
      }, {
        name: 'Sum',
        salary: countData.salary,
        data1: countData.data1,
        data2: countData.data2,
      }]
    }

    const getColorStyle = (column, record) => {
      if (['data1', 'data2'].includes(column.dataIndex)) {
        return {color: record[column.dataIndex] > 0 ? 'red' : 'green'}
      }
      return undefined
    }

    const spanMethod = ({rowIndex, columnIndex}) => {
      if (rowIndex === 0 && columnIndex === 1) {
        return {
          colspan: 2
        }
      }
    };

    return {
      expandable,
      scroll,
      columns,
      data,
      summary,
      getColorStyle,
      spanMethod
    }
  },
}
</script>
```

## 示例：调整列宽

### 说明
使用 `column-resizable` 属性开启列宽调整。建议初始设置除最后一列外其他列的默认列宽。




```vue
<template>
  <a-table :columns="columns" :data="data" column-resizable :bordered="{cell:true}"></a-table>
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const columns = reactive([
      {
        title: 'Name',
        dataIndex: 'name',
        width: 150,
        minWidth: 100,
      },
      {
        title: 'Salary',
        dataIndex: 'salary',
        width: 120,
        minWidth: 80,
      },
      {
        title: 'Address',
        dataIndex: 'address',
        width: 300,
      },
      {
        title: 'Email',
        dataIndex: 'email',
      },
    ]);
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    return {
      columns,
      data
    }
  },
}
</script>
```

## 示例：可拖拽表格

### 说明
（实验性）
开启表格行可拖拽功能




```vue
<template>
  <a-table :columns="columns" :data="data" @change="handleChange" :draggable="{}"></a-table>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const columns = reactive([
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
    ]);
    const data = ref([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);
    const handleChange = (_data) => {
      console.log(_data);
      data.value = _data
    }

    return {
      columns,
      data,
      handleChange
    }
  },
}
</script>
```

## 示例：拖拽锚点

### 说明
（实验性）
开启锚点拖拽功能




```vue
<template>
  <a-table :columns="columns" :data="data" @change="handleChange" :draggable="{ type: 'handle', width: 40 }" />
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const columns = reactive([
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
    ]);
    const data = ref([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);
    const handleChange = (_data) => {
      console.log(_data);
      data.value = _data
    }

    return {
      columns,
      data,
      handleChange
    }
  },
}
</script>
```

## 示例：分组表头

### 说明
`columns` 内可以设置 `children`，用于表头分组。




```vue
<template>
  <a-table :columns="columns" :data="data" :bordered="{headerCell:true}"/>
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const columns = [{
      title: 'Name',
      dataIndex: 'name',
      fixed: 'left',
      width: 140,
    }, {
      title: 'User Info',
      children: [{
        title: 'Birthday',
        dataIndex: 'birthday'
      }, {
        title: 'Address',
        children: [{
          title: 'City',
          dataIndex: 'city'
        }, {
          title: 'Road',
          dataIndex: 'road'
        }, {
          title: 'No.',
          dataIndex: 'no'
        }]
      }]
    }, {
      title: 'Information',
      children: [{
        title: 'Email',
        dataIndex: 'email',
      }, {
        title: 'Phone',
        dataIndex: 'phone',
      }]
    }, {
      title: 'Salary',
      dataIndex: 'salary',
      fixed: 'right',
      width: 120
    }];
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      birthday: '1994-04-21',
      city: 'London',
      road: 'Park',
      no: '34',
      phone: '12345678',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      birthday: '1994-05-21',
      city: 'London',
      road: 'Park',
      no: '37',
      phone: '12345678',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      birthday: '1992-02-11',
      city: 'Paris',
      road: 'Arco',
      no: '67',
      phone: '12345678',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      birthday: '1991-06-21',
      city: 'London',
      road: 'Park',
      no: '317',
      phone: '12345678',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      birthday: '1996-08-21',
      city: 'Paris',
      road: 'Park',
      no: '114',
      phone: '12345678',
      email: 'william.smith@example.com'
    }]);

    return {
      columns,
      data
    }
  },
}
</script>
```

## 示例：分组表头与固定列

### 说明
分组表头使用固定列时，需要优先指定数据列为固定列。
如果一个分组下的所有数据列都是固定列，此时可以设置分组列为固定列，宽度为子列宽度之和。




```vue
<template>
  <a-table :columns="columns" :data="data" :bordered="{cell:true}" :scroll="{ x: 2000 }"/>
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const columns = [{
      title: 'Name',
      dataIndex: 'name',
      fixed: 'left',
      width: 140,
    }, {
      title: 'User Info',
      children: [{
        title: 'Birthday',
        dataIndex: 'birthday',
        fixed: 'left',
        width: 200,
      }, {
        title: 'Address',
        children: [{
          title: 'City',
          dataIndex: 'city',
          fixed: 'left',
          width: 100,
        }, {
          title: 'Road',
          dataIndex: 'road',
        }, {
          title: 'No.',
          dataIndex: 'no',
        }]
      }]
    }, {
      title: 'Information',
      children: [{
        title: 'Email',
        dataIndex: 'email',
      }, {
        title: 'Phone',
        dataIndex: 'phone',
      }]
    }, {
      title: 'Salary',
      dataIndex: 'salary',
      fixed: 'right',
      width: 120
    }];
    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      birthday: '1994-04-21',
      city: 'London',
      road: 'Park',
      no: '34',
      phone: '12345678',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      birthday: '1994-05-21',
      city: 'London',
      road: 'Park',
      no: '37',
      phone: '12345678',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      birthday: '1992-02-11',
      city: 'Paris',
      road: 'Arco',
      no: '67',
      phone: '12345678',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      birthday: '1991-06-21',
      city: 'London',
      road: 'Park',
      no: '317',
      phone: '12345678',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      birthday: '1996-08-21',
      city: 'Paris',
      road: 'Park',
      no: '114',
      phone: '12345678',
      email: 'william.smith@example.com'
    }]);

    return {
      columns,
      data
    }
  },
}
</script>
```

## 示例：可编辑表格

### 说明
可以在使用插槽获得的数据，修改 `data` 中的数据，达到可编辑表格的功能。
`2.25.0` 版本后可以直接修改插槽传出的 `record` 变量。这个 `record` 变量是传入的 `data` 中对应数据的引用，请保证 `data` 为 Reactive 类型。




```vue
<template>
  <a-table :columns="columns" :data="data">
    <template #name="{ rowIndex }">
      <a-input v-model="data[rowIndex].name" />
    </template>
    <template #province="{ rowIndex }">
      <a-select v-model="data[rowIndex].province" @change="()=>handleChange(rowIndex)">
        <a-option v-for="value of Object.keys(options)">{{value}}</a-option>
      </a-select>
    </template>
    <template #city="{ rowIndex }">
      <a-select :options="options[data[rowIndex].province] || []" v-model="data[rowIndex].city" />
    </template>
  </a-table>
  <!-- support from v2.25.0  -->
  <a-table :columns="columns" :data="data" style="margin-top: 20px">
    <template #name="{ record, rowIndex }">
      <a-input v-model="record.name" />
    </template>
    <template #province="{ record,rowIndex }">
      <a-select v-model="record.province" @change="()=>{record.city=''}">
        <a-option v-for="value of Object.keys(options)">{{value}}</a-option>
      </a-select>
    </template>
    <template #city="{ record,rowIndex }">
      <a-select :options="options[record.province] || []" v-model="record.city" />
    </template>
  </a-table>
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const options = {
      Beijing: ['Haidian', 'Chaoyang', 'Changping'],
      Sichuan: ['Chengdu', 'Mianyang', 'Aba'],
      Guangdong: ['Guangzhou', 'Shenzhen', 'Shantou']
    }
    const columns = [{
      title: 'Name',
      dataIndex: 'name',
      slotName: 'name'
    }, {
      title: 'Salary',
      dataIndex: 'salary',
    }, {
      title: 'Address',
      dataIndex: 'address',
    }, {
      title: 'Province',
      dataIndex: 'province',
      slotName: 'province'
    }, {
      title: 'City',
      dataIndex: 'city',
      slotName: 'city'
    }, {
      title: 'Email',
      dataIndex: 'email',
    }];

    const data = reactive([{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      province: 'Beijing',
      city: 'Haidian',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      province: 'Sichuan',
      city: 'Mianyang',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }]);

    const handleChange = (rowIndex) => {
      data[rowIndex].city = ''
    }
    return {
      options,
      columns,
      data,
      handleChange
    }
  },
}
</script>
```

## 示例：自定义渲染

### 说明
通过 `#columns` 插槽和 `<a-table-column>` 组件可以使用模板的方法自定义列渲染。
**注意**：在使用 `#columns` 插槽后，将会屏蔽 `columns` 属性




```vue
<template>
  <a-table :columns="columns" :data="data">
    <template #optional="{ record }">
      <a-button @click="$modal.info({ title:'Name', content:record.name })">view</a-button>
    </template>
  </a-table>
  <a-table :data="data" style="margin-top: 30px">
    <template #columns>
      <a-table-column title="Name">
        <a-table-column title="First Name" data-index="first"></a-table-column>
        <a-table-column title="Last Name" data-index="last"></a-table-column>
      </a-table-column>
      <a-table-column title="Salary" data-index="salary"></a-table-column>
      <a-table-column title="Address" data-index="address"></a-table-column>
      <a-table-column title="Email" data-index="email"></a-table-column>
      <a-table-column title="Optional">
        <template #cell="{ record }">
          <a-button @click="$modal.info({ title:'Name', content:record.name })">view</a-button>
        </template>
      </a-table-column>
    </template>
  </a-table>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const show = ref(true)

    const columns = [{
      title: 'Name',
      dataIndex: 'name',
    }, {
      title: 'Salary',
      dataIndex: 'salary',
    }, {
      title: 'Address',
      dataIndex: 'address',
    }, {
      title: 'Email',
      dataIndex: 'email',
    }, {
      title: 'Optional',
      slotName: 'optional'
    }];
    const data = [{
      key: '1',
      name: 'Jane Doe',
      first: 'Jane',
      last: 'Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      first: 'Alisa',
      last: 'Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      first: 'Kevin',
      last: 'Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      first: 'Ed',
      last: 'Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      first: 'William',
      last: 'Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }];

    return {
      columns,
      data,
      show
    }
  },
}
</script>
```

## 示例：自定义表格元素

### 说明
可以通过特定插槽自定义表格元素的渲染。仅需要传入表格元素，内部属性会自动附加上去




```vue
<template>
  <a-table :columns="columns" :data="data" row-class="common-row">
    <template #tr>
      <tr class="my-tr" @contextmenu="onContextMenu" />
    </template>
    <template #td>
      <td class="my-td" />
    </template>
  </a-table>
</template>

<script>
export default {
  setup() {
    const onContextMenu = () => {
      console.log('right click')
    }

    const columns = [{
      title: 'Name',
      dataIndex: 'name',
    }, {
      title: 'Salary',
      dataIndex: 'salary',
    }, {
      title: 'Address',
      dataIndex: 'address',
    }, {
      title: 'Email',
      dataIndex: 'email',
    }];
    const data = [{
      key: '1',
      name: 'Jane Doe',
      salary: 23000,
      address: '32 Park Road, London',
      email: 'jane.doe@example.com'
    }, {
      key: '2',
      name: 'Alisa Ross',
      salary: 25000,
      address: '35 Park Road, London',
      email: 'alisa.ross@example.com'
    }, {
      key: '3',
      name: 'Kevin Sandra',
      salary: 22000,
      address: '31 Park Road, London',
      email: 'kevin.sandra@example.com'
    }, {
      key: '4',
      name: 'Ed Hellen',
      salary: 17000,
      address: '42 Park Road, London',
      email: 'ed.hellen@example.com'
    }, {
      key: '5',
      name: 'William Smith',
      salary: 27000,
      address: '62 Park Road, London',
      email: 'william.smith@example.com'
    }];

    return {
      columns,
      data,
      onContextMenu,
    }
  },
}
</script>
```

## 示例：虚拟列表

### 说明
设置 `virtual-list-props` 开启虚拟列表功能。
目前虚拟滚动表格受限比较多，开启虚拟滚动后不能使用展开行、树形数据、固定列等功能




```vue
<template>
  <a-table :columns="columns" :data="data"  :row-selection="rowSelection"  :virtual-list-props="{height:400}" :pagination="false" :scroll="{x:1000}" />
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
        fixed: 'left',
        width: 140
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
    const data = reactive(Array(1000).fill(null).map((_, index) => ({
      key: String(index),
      name: `User ${index + 1}`,
      address: '32 Park Road, London',
      email: `user.${index + 1}@example.com`
    })));
    const rowSelection = {
      type: 'checkbox',
      showCheckedAll: true
    };

    return {
      columns,
      data,
      rowSelection
    }
  },
}
</script>
```

## API


### `<table>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|columns|表格的列描述信息|`TableColumnData[]`|`[]`||
|data|表格的数据|`TableData[]`|`[]`||
|bordered|是否显示边框|`boolean \| TableBorder`|`true`||
|hoverable|是否显示选中效果|`boolean`|`true`||
|stripe|是否开启斑马纹效果|`boolean`|`false`||
|size|表格的大小|`'mini' \| 'small' \| 'medium' \| 'large'`|`'large'`||
|table-layout-fixed|表格的 table-layout 属性设置为 fixed，设置为 fixed 后，表格的宽度不会被内容撑开超出 100%。|`boolean`|`false`||
|loading|是否为加载中状态|`boolean\|object`|`false`||
|row-selection|表格的行选择器配置|`TableRowSelection`|`-`||
|expandable|表格的展开行配置|`TableExpandable`|`-`||
|scroll|表格的滚动属性配置。`2.13.0` 版本增加字符型值的支持。`2.20.0` 版本增加 `minWidth`,`maxHeight` 的支持。|`{  x?: number \| string;  y?: number \| string;  minWidth?: number \| string;  maxHeight?: number \| string;}`|`-`||
|pagination|分页的属性配置|`boolean \| PaginationProps`|`true`||
|page-position|分页选择器的位置|`'tl' \| 'top' \| tr' \| 'bl' \| 'bottom' \| 'br'`|`'br'`||
|indent-size|树形表格的缩进距离|`number`|`16`||
|row-key|表格行 `key` 的取值字段|`string`|`'key'`||
|show-header|是否显示表头|`boolean`|`true`||
|virtual-list-props|传递虚拟列表属性，传入此参数以开启虚拟滚动 [VirtualListProps](#VirtualListProps)|`VirtualListProps`|`-`||
|span-method|单元格合并方法（索引从数据项开始计数）|`(data: {  record: TableData;  column: TableColumnData \| TableOperationColumn;  rowIndex: number;  columnIndex: number;}) => { rowspan?: number; colspan?: number } \| void`|`-`|2.10.0|
|span-all|是否让合并方法的索引包含所有|`boolean`|`false`|2.18.0|
|load-more|数据懒加载函数，传入时开启懒加载功能|`(record: TableData, done: (children?: TableData[]) => void) => void`|`-`|2.13.0|
|filter-icon-align-left|筛选图标是否左对齐|`boolean`|`false`|2.13.0|
|hide-expand-button-on-empty|是否在子树为空时隐藏展开按钮|`boolean`|`false`|2.14.0|
|row-class|表格行元素的类名。`2.34.0` 版本增加函数值支持|`string\| any[]\| Record<string, any>\| ((record: TableData, rowIndex: number) => any)`|`-`|2.16.0|
|draggable|表格拖拽排序的配置|`TableDraggable`|`-`|2.16.0|
|column-resizable|是否允许调整列宽|`boolean`|`false`|2.16.0|
|summary|显示表尾总结行|`boolean\| ((params: {    columns: TableColumnData[];    data: TableData[];  }) => TableData[])`|`-`|2.21.0|
|summary-text|总结行的首列文字|`string`|`'Summary'`|2.21.0|
|summary-span-method|总结行的单元格合并方法|`(data: {  record: TableData;  column: TableColumnData \| TableOperationColumn;  rowIndex: number;  columnIndex: number;}) => { rowspan?: number; colspan?: number } \| void`|`-`|2.21.0|
|selected-keys|已选择的行（受控模式）优先于 `rowSelection`|`(string \| number)[]`|`-`|2.25.0|
|default-selected-keys|默认已选择的行（非受控模式）优先于 `rowSelection`|`(string \| number)[]`|`-`|2.25.0|
|expanded-keys|显示的展开行、子树（受控模式）优先于 `expandable`|`(string \| number)[]`|`-`|2.25.0|
|default-expanded-keys|默认显示的展开行、子树（非受控模式）优先于 `expandable`|`(string \| number)[]`|`-`|2.25.0|
|default-expand-all-rows|是否默认展开所有的行|`boolean`|`false`|2.25.0|
|sticky-header|是否开启表头吸顶|`boolean\|number`|`false`|2.30.0|
|scrollbar|是否开启虚拟滚动条|`boolean \| ScrollbarProps`|`true`|2.38.0|
|show-empty-tree|是否展示空子树|`boolean`|`false`|2.51.0|
### `<table>` 事件

|事件名|描述|参数|版本|
|---|---|---|:---|
|expand|点击展开行时触发|rowKey: `string \| number`<br>record: `TableData`||
|expanded-change|已展开的数据行发生改变时触发|rowKeys: `(string \| number)[]`||
|select|点击行选择器时触发|rowKeys: `string \| number[]`<br>rowKey: `string \| number`<br>record: `TableData`||
|select-all|点击全选选择器时触发|checked: `boolean`||
|selection-change|已选择的数据行发生改变时触发|rowKeys: `(string \| number)[]`||
|sorter-change|排序规则发生改变时触发|dataIndex: `string`<br>direction: `string`||
|filter-change|过滤选项发生改变时触发|dataIndex: `string`<br>filteredValues: `string[]`||
|page-change|表格分页发生改变时触发|page: `number`||
|page-size-change|表格每页数据数量发生改变时触发|pageSize: `number`||
|change|表格数据发生变化时触发|data: `TableData[]`<br>extra: `TableChangeExtra`<br>currentData: `TableData[]`|2.40.0 增加 currentData|
|cell-mouse-enter|单元格 hover 进入时触发|record: `TableData`<br>column: `TableColumnData`<br>ev: `Event`||
|cell-mouse-leave|单元格 hover 退出时触发|record: `TableData`<br>column: `TableColumnData`<br>ev: `Event`||
|cell-click|点击单元格时触发|record: `TableData`<br>column: `TableColumnData`<br>ev: `Event`||
|row-click|点击行数据时触发|record: `TableData`<br>ev: `Event`||
|header-click|点击表头数据时触发|column: `TableColumnData`<br>ev: `Event`||
|column-resize|调整列宽时触发|dataIndex: `string`<br>width: `number`|2.28.0|
|row-dblclick|双击行数据时触发|record: `TableData`<br>ev: `Event`||
|cell-dblclick|双击单元格时触发|record: `TableData`<br>column: `TableColumnData`<br>ev: `Event`||
|row-contextmenu|右击行数据时触发|record: `TableData`<br>ev: `Event`||
|cell-contextmenu|右击单元格时触发|record: `TableData`<br>column: `TableColumnData`<br>ev: `Event`||
### `<table>` 方法

|方法名|描述|参数|返回值|版本|
|---|---|---|---|:---|
|selectAll|设置全选状态|checked: ` boolean `|-|2.22.0|
|select|设置行选择器状态|rowKey: ` string \| number \| (string \| number)[] `<br>checked: ` boolean `|-|2.31.0|
|expandAll|设置全部展开状态|checked: ` boolean `|-|2.31.0|
|expand|设置展开状态|rowKey: ` string \| number \| (string \| number)[] `<br>checked: ` boolean `|-|2.31.0|
|resetFilters|重置列的筛选器|dataIndex: ` string \| string[] `|-|2.31.0|
|clearFilters|清空列的筛选器|dataIndex: ` string \| string[] `|-|2.31.0|
|resetSorters|重置列的排序|-|-|2.31.0|
|clearSorters|清空列的排序|-|-|2.31.0|
### `<table>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|th|自定义 th 元素|column: `TableColumnData`|2.26.0|
|thead|自定义 thead 元素|-|2.26.0|
|empty|空白展示|-||
|summary-cell|总结行|column: `TableColumnData`<br>record: `TableData`<br>rowIndex: `number`|2.23.0|
|pagination-right|分页器右侧内容|-|2.18.0|
|pagination-left|分页器左侧内容|-|2.18.0|
|td|自定义 td 元素|column: `TableColumnData`<br>record: `TableData`<br>rowIndex: `number`|2.16.0|
|tr|自定义 tr 元素|record: `TableData`<br>rowIndex: `number`|2.16.0|
|tbody|自定义 tbody 元素|-|2.16.0|
|drag-handle-icon|拖拽锚点图标|-|2.16.0|
|footer|表格底部|-||
|expand-row|展开行内容|record: `TableData`||
|expand-icon|展开行图标|expanded: `boolean`<br>record: `TableData`||
|columns|表格列定义。启用时会屏蔽 columns 属性|-||




### `<table-column>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|data-index|列信息的标识，对应TableData中的数据|`string`|`-`||
|title|列标题|`string`|`-`||
|width|列宽度|`number`|`-`||
|min-width|最小列宽|`number`|`-`||
|align|对齐方向|`TableColumnData['align']`|`-`||
|fixed|固定位置|`TableColumnData['fixed']`|`-`||
|ellipsis|是否显示为省略|`boolean`|`false`||
|sortable|排序相关选项|`TableSortable`|`-`||
|filterable|过滤相关选项|`TableFilterable`|`-`||
|cell-class|自定义单元格类名|`ClassName`|`-`|2.36.0|
|header-cell-class|自定义表头单元格类名|`ClassName`|`-`|2.36.0|
|body-cell-class|自定义内容单元格类名|`ClassName \| ((record: TableData) => ClassName)`|`-`|2.36.0|
|summary-cell-class|自定义总结栏单元格类名|`ClassName \| ((record: TableData) => ClassName)`|`-`|2.36.0|
|cell-style|自定义单元格样式|`CSSProperties`|`-`|2.11.0|
|header-cell-style|自定义表头单元格样式|`CSSProperties`|`-`|2.29.0|
|body-cell-style|自定义内容单元格样式|`CSSProperties \| ((record: TableData) => CSSProperties)`|`-`|2.29.0|
|summary-cell-style|自定义总结栏单元格样式|`CSSProperties \| ((record: TableData) => CSSProperties)`|`-`|2.30.0|
|index|用于手动指定选项的 index。2.26.0 版本后不再需要手动指定|`number`|`-`|2.20.2|
|tooltip|在省略时是否显示文字提示|`boolean\|object`|`false`|2.26.0|
### `<table-column>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|filter-icon|筛选按钮图标|-|2.23.0|
|filter-content|自定义筛选弹出框内容|filterValue: `string[]`<br>setFilterValue: `(filterValue: string[]) => void`<br>handleFilterConfirm: `(event: Event) => void`<br>handleFilterReset: `(event: Event) => void`|2.23.0|
|title|标题|-||
|cell|单元格|record: `TableData`<br>column: `TableColumnData`<br>rowIndex: `number`||



## Type

```ts
type Filters = Record<string, string[]>;

type Sorter = { filed: string; direction: 'ascend' | 'descend' } | Record<string, never>;
```


### TableData

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|key|数据行的key|`string`|`-`||
|expand|扩展行内容|`string \| RenderFunction`|`-`||
|children|子数据|`TableData[]`|`-`||
|disabled|是否禁用行选择器|`boolean`|`false`||
|isLeaf|是否是叶子节点|`boolean`|`false`|2.13.0|



### TableSortable

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|sortDirections|支持的排序方向|`('ascend' \| 'descend')[]`|`-`|
|sorter|排序函数。设置为 `true` 可关闭内部排序。2.19.0 版本修改传出数据。|`((        a: TableData,        b: TableData,        extra: { dataIndex: string; direction: 'ascend' \| 'descend' }      ) => number)    \| boolean`|`-`|
|sortOrder|排序方向|`'ascend' \| 'descend' \| ''`|`-`|
|defaultSortOrder|默认排序方向（非受控模式）|`'ascend' \| 'descend' \| ''`|`-`|



### TableFilterData

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|text|筛选数据选项的内容|`string \| RenderFunction`|`-`|
|value|筛选数据选项的值|`string`|`-`|



### TableFilterable

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|filters|筛选数据|`TableFilterData[]`|`-`||
|filter|筛选函数|`(filteredValue: string[], record: TableData) => boolean`|`-`||
|multiple|是否支持多选|`boolean`|`false`||
|filteredValue|筛选项|`string[]`|`-`||
|defaultFilteredValue|默认筛选项|`string[]`|`-`||
|renderContent|筛选框的内容|`(data: {    filterValue: string[];    setFilterValue: (filterValue: string[]) => void;    handleFilterConfirm: (event: Event) => void;    handleFilterReset: (event: Event) => void;  }) => VNodeChild`|`-`||
|icon|筛选按钮的图标|`RenderFunction`|`-`||
|triggerProps|筛选框的弹出框配置|`TriggerProps`|`-`||
|alignLeft|筛选图标是否左对齐|`boolean`|`false`|2.13.0|



### TableColumnData

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|dataIndex|列信息的标识，对应 `TableData` 中的数据|`string`|`-`||
|title|列标题|`string \| RenderFunction`|`-`||
|width|列宽度|`number`|`-`||
|minWidth|最小列宽|`number`|`-`||
|align|对齐方向|`'left' \| 'center' \| 'right'`|`-`||
|fixed|固定位置|`'left' \| 'right'`|`-`||
|ellipsis|是否显示省略号|`boolean`|`false`||
|tooltip|是否在显示省略号时显示文本提示。可填入 tooltip 组件属性|`boolean \| Record<string, any>`|`-`|2.26.0|
|sortable|排序相关选项|`TableSortable`|`-`||
|filterable|过滤相关选项|`TableFilterable`|`-`||
|children|表头子数据，用于表头分组|`TableColumnData[]`|`-`||
|cellClass|自定义单元格类名|`ClassName`|`-`|2.36.0|
|headerCellClass|自定义表头单元格类名|`ClassName`|`-`|2.36.0|
|bodyCellClass|自定义内容单元格类名|`ClassName \| ((record: TableData) => ClassName)`|`-`|2.36.0|
|summaryCellClass|自定义总结栏单元格类名|`ClassName \| ((record: TableData) => ClassName)`|`-`|2.36.0|
|cellStyle|自定义单元格样式|`CSSProperties`|`-`|2.11.0|
|headerCellStyle|自定义表头单元格样式|`CSSProperties`|`-`|2.29.0|
|bodyCellStyle|自定义内容单元格样式|`CSSProperties \| ((record: TableData) => CSSProperties)`|`-`|2.29.0|
|summaryCellStyle|自定义总结栏单元格样式|`CSSProperties \| ((record: TableData) => CSSProperties)`|`-`|2.30.0|
|render|自定义列单元格的渲染|`(data: {    record: TableData;    column: TableColumnData;    rowIndex: number;  }) => VNodeChild`|`-`||
|slotName|设置当前列的渲染插槽的名字。插槽参数同 #cell|`string`|`-`|2.18.0|
|titleSlotName|设置当前列的标题的渲染插槽的名字|`string`|`-`|2.23.0|



### TableBorder

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|wrapper|是否展示外边框|`boolean`|`false`|
|cell|是否展示单元格边框（表头+主体）|`boolean`|`false`|
|headerCell|是否展示表头单元格边框|`boolean`|`false`|
|bodyCell|是否展示主体单元格边框|`boolean`|`false`|



### TableRowSelection

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|type|行选择器的类型|`'checkbox' \| 'radio'`|`-`||
|selectedRowKeys|已选择的行（受控模式）|`BaseType[]`|`-`||
|defaultSelectedRowKeys|默认已选择的行（非受控模式）|`BaseType[]`|`-`||
|showCheckedAll|是否显示全选选择器|`boolean`|`false`||
|title|列标题|`string`|`-`||
|width|列宽度|`number`|`-`||
|fixed|是否固定|`boolean`|`false`||
|checkStrictly|是否开启严格选择模式|`boolean`|`true`|2.29.0|
|onlyCurrent|是否仅展示当前页的 keys（切换分页时清空 keys）|`boolean`|`false`|2.32.0|



### TableExpandable

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|expandedRowKeys|显示的展开行（受控模式）|`BaseType[]`|`-`|
|defaultExpandedRowKeys|默认显示的展开行（非受控模式）|`BaseType[]`|`-`|
|defaultExpandAllRows|是否默认展开所有的行|`boolean`|`false`|
|expandedRowRender|自定义展开行内容|`(record: TableData) => VNodeChild`|`-`|
|icon|展开图标|`(expanded: boolean, record: TableData) => VNodeChild`|`-`|
|title|列标题|`string`|`-`|
|width|列宽度|`number`|`-`|
|fixed|是否固定|`boolean`|`false`|



### TableDraggable

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|拖拽类型|`'row' \| 'handle'`|`-`|
|title|列标题|`string`|`-`|
|width|列宽度|`number`|`-`|
|fixed|是否固定|`boolean`|`false`|



### TableChangeExtra

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|触发类型|`'pagination' \| 'sorter' \| 'filter' \| 'drag'`|`-`|
|page|页码|`number`|`-`|
|pageSize|每页数据数|`number`|`-`|
|sorter|排序信息|`Sorter`|`-`|
|filters|筛选信息|`Filters`|`-`|
|dragTarget|拖拽信息|`TableData`|`-`|




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

### 1. 关于元素插槽的使用

table 组件提供了内部元素的自定义插槽，这些插槽不同于普通插槽，对用户传入的内容有一定限制。
因为 vue 的插槽没有提供传出 children 并在 slot 中渲染的方式，我们针对 table 中的元素插槽，做了一些特殊处理，会在用户传入的内容中，附加上原有的 children，保证子元素的正常渲染。
此时需要用户注意，在元素插槽中自定义渲染时，需要传入单一空元素使用，不能在传入的元素中添加内容（参考例 1）。
如果用户需要传入复合元素，可以自定义组件，并指定 default 插槽，然后传入 table 的元素插槽中（参考例 2）。

例 1：
```vue
<!-- Only one element -->
<template>
  <a-table>
    <template #td>
      <td @click="onClick"></td>
    </template>
  </a-table>
</template>
```
例 2：
```vue
<!-- Only one component -->
<template>
  <a-table>
    <template #td>
      <MyTd></MyTd>
    </template>
  </a-table>
</template>
```
```vue
<!-- MyTd.vue -->
<template>
  <td>
    <div>my td content</div>
    <div>
      <slot/>
    </div>
  </td>
</template>
```

### 2. 关于数据中的 `row-key` 设置

表格默认会通过数据中设置的 `key` 字段来唯一定位行数据，在提供数据时请确保行数据中都设置了 `key` 字段。这个字段在开启选择器等功能时为必要字段，如果想要更换默认的字段名，可以修改 `row-key` 进行设置。
