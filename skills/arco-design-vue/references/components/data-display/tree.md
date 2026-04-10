---
name: arco-vue-tree
description: "Arco Design Vue 树 Tree 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-tree>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 树 Tree

来源组件：上游 `web-vue/components/tree`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-tree>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
为每个节点赋予全局唯一的 `key`（必填项），`title` 为该节点显示的内容。




```vue
<template>
  <a-tree
    :data="treeData"
    :default-expanded-keys="['0-0-0']"
    :default-selected-keys="['0-0-0', '0-0-1']"
  />
</template>
<script>
  export default {
    data() {
      return {
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
          title: 'Branch 0-0-0',
          key: '0-0-0',
          disabled: true,
          children: [
            {
              title: 'Leaf',
              key: '0-0-0-0',
            },
            {
              title: 'Leaf',
              key: '0-0-0-1',
            }
          ]
        },
        {
          title: 'Branch 0-0-1',
          key: '0-0-1',
          children: [
            {
              title: 'Leaf',
              key: '0-0-1-0',
            },
          ]
        },
      ],
    },
  ];
</script>
```

## 示例：节点占一行

### 说明
节点占据一整行。



```vue
<template>
  <a-tree blockNode :data="treeData" />
</template>
<script>
  export default {
    data() {
      return {
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
          title: 'Branch 0-0-0',
          key: '0-0-0',
          children: [
            {
              title: 'Leaf',
              key: '0-0-0-0',
            },
            {
              title: 'Leaf',
              key: '0-0-0-1',
            }
          ]
        },
        {
          title: 'Branch 0-0-1',
          key: '0-0-1',
          children: [
            {
              title: 'Leaf',
              key: '0-0-1-0',
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
`Tree` 设置 `multiple` 属性为`true`，可以启用多选。




```vue
<template>
  <a-checkbox
    style="marginBottom: 24px;"
    v-model="multiple"
    @change="() => {
      selectedKeys = [];
    }"
  >
    multiple
  </a-checkbox>
  <br/>
  <a-typography-text>
    Current: {{ selectedKeys?.join(' , ') }}
  </a-typography-text>
  <br/>
  <a-tree
    v-model:selected-keys="selectedKeys"
    :multiple="multiple"
    :data="treeData"
  />
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const selectedKeys = ref([]);
      const multiple = ref(true);
      const treeData = [
        {
          title: 'Trunk 0-0',
          key: '0-0',
          children: [
            {
              title: 'Leaf',
              key: '0-0-1',
            },
            {
              title: 'Branch 0-0-2',
              key: '0-0-2',
              children: [
                {
                  title: 'Leaf',
                  key: '0-0-2-1'
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
                  title: 'Leaf',
                  key: '0-1-1-1',
                },
                {
                  title: 'Leaf',
                  key: '0-1-1-2',
                },
              ]
            },
            {
              title: 'Leaf',
              key: '0-1-2',
            },
          ],
        },
      ];

      return {
        selectedKeys,
        multiple,
        treeData,
      };
    },
  }
</script>
```

## 示例：带复选框的树

### 说明
为 `Tree` 添加 `checkable` 属性即可使树具有复选框功能，可以用 `defaultCheckedKeys` 指定复选框默认选中的节点。




```vue
<template>
  <a-checkbox
    style="marginBottom: 24px;"
    v-model="checkStrictly"
    @change="() => {
      checkedKeys = [];
    }"
  >
    checkStrictly
  </a-checkbox>
  <a-tree
    :checkable="true"
    v-model:checked-keys="checkedKeys"
    :check-strictly="checkStrictly"
    :data="treeData"
  />
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
    const checkedKeys = ref([]);
    const checkStrictly = ref(false);

      return {
        checkedKeys,
        checkStrictly,
        treeData,
      }
    }
  }

  const treeData = [
    {
      title: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Leaf',
          key: '0-0-1',
        },
        {
          title: 'Branch 0-0-2',
          key: '0-0-2',
          disabled: true,
          children: [
            {
              title: 'Leaf',
              key: '0-0-2-1'
            },
            {
              title: 'Leaf',
              key: '0-0-2-2',
              disableCheckbox: true
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
              title: 'Leaf ',
              key: '0-1-1-1',
            },
            {
              title: 'Leaf ',
              key: '0-1-1-2',
            },
          ]
        },
        {
          title: 'Leaf',
          key: '0-1-2',
        },
      ],
    },
  ];
</script>
```

## 示例：双向绑定

### 说明
`selectedKeys` 、 `checkedKeys` 、 `expandedKeys` 属性均可受控，不仅支持 `v-model` ，还可以在对应的 `select` / `check` / `expand` 事件中自行控制如何更新属性值。




```vue
<template>
  <a-button-group style="margin-bottom: 20px;">
    <a-button
      type="primary"
      @click="toggleChecked"
    >
      {{
        checkedKeys?.length ? 'deselect all' : 'select all'
      }}
    </a-button>
    <a-button
      type="primary"
      @click="toggleExpanded"
    >
      {{
        expandedKeys?.length ? 'fold' : 'unfold'
      }}
    </a-button>
  </a-button-group>
  <a-tree
    :checkable="true"
    v-model:selected-keys="selectedKeys"
    v-model:checked-keys="checkedKeys"
    v-model:expanded-keys="expandedKeys"
    @select="onSelect"
    @check="onCheck"
    @expand="onExpand"
    :data="treeData"
  />
</template>
<script>
  import { ref } from 'vue';

  const allCheckedKeys = ['0-0', '0-0-1', '0-0-2', '0-0-2-1', '0-1', '0-1-1', '0-1-2'];
  const allExpandedKeys = ['0-0', '0-1', '0-0-2'];


  export default {
    setup() {
      const selectedKeys = ref([]);
      const checkedKeys = ref([]);
      const expandedKeys = ref([]);


      return {
        selectedKeys,
        checkedKeys,
        expandedKeys,
        treeData,
        toggleChecked() {
          checkedKeys.value = checkedKeys?.value.length ? [] : allCheckedKeys;
        },
        toggleExpanded() {
          expandedKeys.value = expandedKeys?.value.length ? [] : allExpandedKeys;
        },
        onSelect(newSelectedKeys, event) {
          console.log('select: ', newSelectedKeys, event);
        },
        onCheck(newCheckedKeys, event) {
          console.log('check: ', newCheckedKeys, event);
        },
        onExpand(newExpandedKeys, event) {
          console.log('expand: ', newExpandedKeys, event);
        },
      };
    },
  };

  const treeData = [
    {
      title: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Leaf 0-0-1',
          key: '0-0-1',
        },
        {
          title: 'Branch 0-0-2',
          key: '0-0-2',
          children: [
            {
              title: 'Leaf 0-0-2-1',
              key: '0-0-2-1'
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
          title: 'Leaf 0-1-1',
          key: '0-1-1',
        },
        {
          title: 'Leaf 0-1-2',
          key: '0-1-2',
        },
      ],
    },
  ];
</script>
```

## 示例：动态加载

### 说明
动态加载节点。




```vue
<template>
  <a-tree :data="treeData" :load-more="loadMore" />
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const treeData = ref([
        {
          title: 'Trunk 0-0',
          key: '0-0'
        },
        {
          title: 'Trunk 0-1',
          key: '0-1',
          children: [
            {
              title: 'Branch 0-1-1',
              key: '0-1-1'
            }
          ],
        },
      ]);

      const loadMore = (nodeData) => {
        return new Promise((resolve) => {
          setTimeout(() => {
            nodeData.children = [
              { title: `leaf`, key: `${nodeData.key}-1`, isLeaf: true },
            ];
            resolve();
          }, 1000);
        });
      };

      return {
        treeData,
        loadMore,
      };
    }
  }

</script>
```

## 示例：拖拽

### 说明
可拖拽的树节点。




```vue
<template>
  <a-checkbox
    v-model="checked"
    style="margin-bottom: 20px;"
  >
    checkable
  </a-checkbox>
  <a-tree
    class="tree-demo"
    draggable
    blockNode
    :checkable="checked"
    :data="treeData"
    @drop="onDrop"
  />
</template>
<script>
  import { ref } from 'vue';
  export default {
    setup() {
      const treeData = ref(defaultTreeData);
      const checkedKeys = ref([]);
      const checked = ref(false);

      return {
        treeData,
        checkedKeys,
        checked,
        onDrop({ dragNode, dropNode, dropPosition }) {
          const data = treeData.value;
          const loop = (data, key, callback) => {
            data.some((item, index, arr) => {
              if (item.key === key) {
                callback(item, index, arr);
                return true;
              }
              if (item.children) {
                return loop(item.children, key, callback);
              }
              return false;
            });
          };

          loop(data, dragNode.key, (_, index, arr) => {
            arr.splice(index, 1);
          });

          if (dropPosition === 0) {
            loop(data, dropNode.key, (item) => {
              item.children = item.children || [];
              item.children.push(dragNode);
            });
          } else {
            loop(data, dropNode.key, (_, index, arr) => {
              arr.splice(dropPosition < 0 ? index : index + 1, 0, dragNode);
            });
          }
        }
      };
    }
  };

  const defaultTreeData = [
    {
      title: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Leaf 0-0-1',
          key: '0-0-1',
        },
        {
          title: 'Branch 0-0-2',
          key: '0-0-2',
          disableCheckbox: true,
          children: [
            {
              draggable: false,
              title: 'Leaf 0-0-2-1 (Drag disabled)',
              key: '0-0-2-1'
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
          checkable: false,
          children: [
            {
              title: 'Leaf 0-1-1-1',
              key: '0-1-1-1',
            },
            {
              title: 'Leaf 0-1-1-2',
              key: '0-1-1-2',
            },
          ]
        },
        {
          title: 'Leaf 0-1-2',
          key: '0-1-2',
        },
      ],
    },
  ]
</script>
<style scoped>
.tree-demo :deep(.tree-node-dropover) > :deep(.arco-tree-node-title),
.tree-demo :deep(.tree-node-dropover) > :deep(.arco-tree-node-title):hover, {
  animation: blinkBg 0.4s 2;
}

@keyframes blinkBg {
  0% {
    background-color: transparent;
  }

  100% {
    background-color: var(--color-primary-light-1);
  }
}
</style>
```

## 示例：设置回填方式

### 说明
为 `Tree` 添加 `checkedStrategy` 可以设置选中时的回填方式




```vue
<template>
  <a-radio-group
    type='button'
    v-model="checkedStrategy"
    @change="(value) => {
      checkedKeys = []
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
  <br/>
  <a-typography-text style="margin: 24px 0; display: inline-block;">
    Current: {{ checkedKeys?.join(' , ') }}
  </a-typography-text>
  <br/>
  <a-tree
    :checkable="true"
    v-model:checked-keys="checkedKeys"
    :checked-strategy="checkedStrategy"
    :data="treeData"
  />
</template>
<script>
  import { ref } from 'vue';

  const treeData = [
    {
      title: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Leaf',
          key: '0-0-1',
        },
        {
          title: 'Branch 0-0-2',
          key: '0-0-2',
          children: [
            {
              title: 'Leaf',
              key: '0-0-2-1'
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
              title: 'Leaf',
              key: '0-1-1-1',
            },
            {
              title: 'Leaf',
              key: '0-1-1-2',
            },
          ]
        },
        {
          title: 'Leaf',
          key: '0-1-2',
        },
      ],
    },
  ];

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

  export default {
    setup() {
      const checkedKeys = ref([]);
      const checkedStrategy = ref('all');

      return {
        treeData,
        strategyOptions,
        checkedStrategy,
        checkedKeys,
      }
    }
  }
</script>
```

## 示例：显示连接线

### 说明
为 `Tree` 添加 `showLine` 属性即可使树具有连接线




```vue
<template>
  <div>
    <a-typography-text>showLine</a-typography-text>
    <a-switch v-model="showLine" style="margin-left: 12px" />
  </div>
  <a-tree
    :default-selected-keys="['0-0-1']"
    :data="treeData"
    :show-line="showLine"
  />
</template>
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const showLine = ref(true);

      return {
        showLine,
        treeData,
      };
    },
  };

  const treeData = [
    {
      title: 'Trunk 1',
      key: '0-0',
      children: [
        {
          title: 'Trunk 1-0',
          key: '0-0-0',
          children: [
            { title: 'leaf', key: '0-0-0-0' },
            {
              title: 'leaf',
              key: '0-0-0-1',
              children: [{ title: 'leaf', key: '0-0-0-1-0' }],
            },
            { title: 'leaf', key: '0-0-0-2' },
          ],
        },
        {
          title: 'Trunk 1-1',
          key: '0-0-1',
        },
        {
          title: 'Trunk 1-2',
          key: '0-0-2',
          children: [
            { title: 'leaf', key: '0-0-2-0' },
            {
              title: 'leaf',
              key: '0-0-2-1',
            },
          ],
        },
      ],
    },
    {
      title: 'Trunk 2',
      key: '0-1',
    },
    {
      title: 'Trunk 3',
      key: '0-2',
      children: [
        {
          title: 'Trunk 3-0',
          key: '0-2-0',
          children: [
            { title: 'leaf', key: '0-2-0-0' },
            { title: 'leaf', key: '0-2-0-1' },
          ],
        },
      ],
    },
  ];
</script>
```

## 示例：不同尺寸

### 说明
不同尺寸的树。




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
  <a-tree
    style="margin-right: 20px;"
    :blockNode="true"
    :checkable="true"
    :size="size"
    :data="treeData" />
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
      title: 'Trunk 0-0',
      key: '0-0',
      children: [
        {
          title: 'Branch 0-0-0',
          key: '0-0-0',
          children: [
            {
              title: 'Leaf',
              key: '0-0-0-0',
            },
            {
              title: 'Leaf',
              key: '0-0-0-1',
            }
          ]
        },
        {
          title: 'Branch 0-0-1',
          key: '0-0-1',
          children: [
            {
              title: 'Leaf',
              key: '0-0-1-0',
            },
          ]
        },
      ],
    },
  ];
</script>
```

## 示例：定制节点图标

### 说明
节点图标可以通过 `tree` 的 `icon` 插槽全局指定，也可以通过节点的 `icon` 属性单独指定。




```vue
<template>
  <a-tree :data="treeData">
    <template #icon>
      <IconStar />
    </template>
  </a-tree>
</template>
<script>
  import { h } from 'vue';
  import { IconStar, IconDriveFile } from '@arco-design/web-vue/es/icon';

  export default {
    components: {
      IconStar
    },
    setup() {
      return {
        treeData,
      };
    },
  };

  const treeData = [
    {
      title: 'Trunk',
      key: 'node1',
      children: [
        {
          title: 'Leaf',
          key: 'node2',
        },
      ],
    },
    {
      title: 'Trunk',
      key: 'node3',
      children: [
        {
          title: 'Leaf',
          key: 'node4',
          icon: () => h(IconDriveFile),
        },
        {
          title: 'Leaf',
          key: 'node5',
          icon: () => h(IconDriveFile),
        },
      ],
    },
  ];
</script>
```

## 示例：定制额外节点

### 说明
`Tree` 提供了名为 `extra` 的 `Slot`, 可以在节点上定制额外的内容。




```vue
<template>
  <div style="width: 500px; padding: 2px; overflow: auto">
    <a-tree
      :blockNode="true"
      :checkable="true"
      :data="treeData"
    >
      <template #extra="nodeData">
        <IconPlus
          style="position: absolute; right: 8px; font-size: 12px; top: 10px; color: #3370ff;"
          @click="() => onIconClick(nodeData)"
        />
      </template>
    </a-tree>
  </div>
</template>
<script>
 import {ref} from 'vue';
 import { IconPlus } from '@arco-design/web-vue/es/icon';

 export default {
   components: {
     IconPlus,
   },
   setup() {
     function onIconClick(nodeData) {
      const children = nodeData.children || []
      children.push({
        title: 'new tree node',
        key: nodeData.key + '-' + (children.length + 1)
      })
      nodeData.children = children

      treeData.value = [...treeData.value];
    }

    const treeData = ref(
      [
        {
          title: 'Trunk',
          key: '0-0',
          children: [
            {
              title: 'Leaf',
              key: '0-0-1',
            },
            {
              title: 'Branch',
              key: '0-0-2',
              children: [
                {
                  title: 'Leaf',
                  key: '0-0-2-1'
                }
              ]
            },
          ],
        },
        {
          title: 'Trunk',
          key: '0-1',
          children: [
            {
              title: 'Branch',
              key: '0-1-1',
              children: [
                {
                  title: 'Leaf',
                  key: '0-1-1-1',
                },
                {
                  title: 'Leaf',
                  key: '0-1-1-2',
                },
              ]
            },
            {
              title: 'Leaf',
              key: '0-1-2',
            },
          ],
        },
      ]
    );

    return {
      onIconClick,
      treeData,
    };
   }
 };
</script>
```

## 示例：定制组件图标

### 说明
节点的图标 `loadingIcon`,  `switcherIcon`，同时支持在 `tree` 和 `node` 两个纬度上定制，其中 `node` 的优先级较高。




```vue
<template>
  <a-tree :data="treeData" show-line>
     <template #switcher-icon="node, { isLeaf }">
      <IconDown v-if="!isLeaf" />
      <IconStar v-if="isLeaf" />
    </template>
  </a-tree>
</template>

<script>
  import { h } from 'vue';
  import { IconDriveFile, IconDown, IconStar } from '@arco-design/web-vue/es/icon';

  export default {
    components: {
      IconDown,
      IconStar
    },
    setup() {
      return {
        treeData,
      };
    },
  };

  const treeData = [
    {
      title: 'Trunk',
      key: 'node1',
      children: [
        {
          title: 'Leaf',
          key: 'node2',
        },
      ],
    },
    {
      title: 'Trunk',
      key: 'node3',
      children: [
        {
          title: 'Leaf',
          key: 'node4',
          switcherIcon: () => h(IconDriveFile),
        },
        {
          title: 'Leaf',
          key: 'node5',
          switcherIcon: () => h(IconDriveFile),
        },
      ],
    },
  ];
</script>
```

## 示例：虚拟列表

### 说明
通过指定 `virtualListProps` 来开启虚拟列表，在大量数据时获得高性能表现。



```vue
<template>
  <a-button
    type="primary"
    :style="{ marginBottom: '20px' }"
    @click="scrollIntoView"
  >
    Scroll to 0-0-2-2, i.e. the 26th.
  </a-button>
  <a-tree
    ref="treeRef"
    blockNode
    checkable
    :data="treeData"
    :virtualListProps="{
      height: 200,
    }"
  />
</template>
<script>
  import { ref } from 'vue';
  export default {
    setup() {
      const treeRef = ref();
      const treeData = loop();
      return {
        treeRef,
        treeData,
        scrollIntoView() {
          treeRef.value && treeRef.value.scrollIntoView({ key: '0-0-2-2' });
        }
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

## 示例：搜索树

### 说明
展示如何实现搜索树的效果。




```vue
<template>
  <div>
    <a-input-search
      style="margin-bottom: 8px; max-width: 240px"
      v-model="searchKey"
    />
    <a-tree :data="treeData">
      <template #title="nodeData">
        <template v-if="index = getMatchIndex(nodeData?.title), index < 0">{{ nodeData?.title }}</template>
        <span v-else>
          {{ nodeData?.title?.substr(0, index) }}
          <span style="color: var(--color-primary-light-4);">
            {{ nodeData?.title?.substr(index, searchKey.length) }}
          </span>{{ nodeData?.title?.substr(index + searchKey.length) }}
        </span>
      </template>
    </a-tree>
  </div>
</template>
<script>
  import { ref, computed } from 'vue';

  const originTreeData = [
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

  export default {
    setup() {
      const searchKey = ref('');
      const treeData = computed(() => {
        if (!searchKey.value) return originTreeData;
        return searchData(searchKey.value);
      })

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

        return loop(originTreeData);
      }

      function getMatchIndex(title) {
        if (!searchKey.value) return -1;
        return title.toLowerCase().indexOf(searchKey.value.toLowerCase());
      }

      return {
        searchKey,
        treeData,
        getMatchIndex,
      }
    }
  }
</script>
```

## 示例：自定义 data 的字段名称

### 说明
通过 `fieldNames` 字段可以自定义 data 的字段名。




```vue
<template>
  <a-tree
    :default-selected-keys="['0-0-1']"
    :fieldNames="{
      key: 'value',
      title: 'label',
      children: 'items',
      icon: 'customIcon'
    }"
    :data="treeData"
  />
</template>
<script>
  import { h } from 'vue';
  import { IconStar, IconDriveFile } from '@arco-design/web-vue/es/icon';
  export default {
    data() {
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
          customIcon: () => h(IconDriveFile),
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
                      customIcon: () => h(IconStar),
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

## API


### `<tree>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|size|尺寸|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|block-node|节点是否占据一行|`boolean`|`false`||
|default-expand-all|是否默认展开父节点|`boolean`|`true`||
|multiple|是否支持多选|`boolean`|`false`||
|checkable|是否在节点前添加复选框，从 `2.27.0` 开始支持函数格式|`boolean\| ((    node: TreeNodeData,    info: {      level: number;      isLeaf: boolean;    }  ) => boolean)`|`false`||
|selectable|是否支持选择，从 `2.27.0` 开始支持函数格式|`boolean\| ((    node: TreeNodeData,    info: {      level: number;      isLeaf: boolean;    }  ) => boolean)`|`true`||
|check-strictly|是否取消父子节点关联|`boolean`|`false`||
|checked-strategy|定制回填方式 <br/> all: 返回所有选中的节点  <br/> parent: 父子节点都选中时只返回父节点 <br/> child: 只返回子节点|`'all' \| 'parent' \| 'child'`|`'all'`||
|default-selected-keys|默认选中的树节点|`Array<string \| number>`|`-`||
|selected-keys **(v-model)**|选中的树节点|`Array<string \| number>`|`-`||
|default-checked-keys|默认选中复选框的树节点|`Array<string \| number>`|`-`||
|checked-keys **(v-model)**|选中复选框的树节点|`Array<string \| number>`|`-`||
|default-expanded-keys|默认展开的节点|`Array<string \| number>`|`-`||
|expanded-keys **(v-model)**|展开的节点|`Array<string \| number>`|`-`||
|data|传入`data`,生成对应的树结构|`TreeNodeData[]`|`[]`||
|field-names|指定节点数据中的字段名|`TreeFieldNames`|`-`||
|show-line|是否展示连接线|`boolean`|`false`||
|load-more|异步加载数据的回调，返回一个 `Promise`|`(node: TreeNodeData) => Promise<void>`|`-`||
|draggable|是否可以拖拽|`boolean`|`false`||
|allow-drop|拖拽时是否允许在某节点上释放|`(options: {  dropNode: TreeNodeData;  dropPosition: -1 \| 0 \| 1;}) => boolean`|`-`||
|virtual-list-props|传递虚拟列表属性，传入此参数以开启虚拟滚动，[VirtualListProps](#VirtualListProps)|`VirtualListProps`|`-`||
|default-expand-selected|是否默认展开已选中节点的父节点|`boolean`|`false`|2.9.0|
|default-expand-checked|是否默认展开已选中复选框节点的父节点|`boolean`|`false`|2.9.0|
|auto-expand-parent|是否自动展开已展开节点的父节点|`boolean`|`true`|2.9.0|
|half-checked-keys **(v-model)**|半选状态的节点.仅在 checkable 且 checkStrictly 时生效|`Array<string \| number>`|`-`|2.19.0|
|only-check-leaf|开启后 checkedKeys 只处理叶子节点，父节点状态由子节点决定（仅在 checkable 且 checkStrictly 为 false 时生效）|`boolean`|`false`|2.21.0|
|animation|是否开启展开时的过渡动效|`boolean`|`true`|2.21.0|
|action-on-node-click|点击节点的时候触发的动作|`'expand'`|`-`|2.27.0|
### `<tree>` 事件

|事件名|描述|参数|
|---|---|---|
|select|点击树节点时触发|selectedKeys: `Array<string \| number>`<br>data: `{ selected?: boolean; selectedNodes: TreeNodeData[]; node?: TreeNodeData; e?: Event; }`|
|check|点击树节点复选框时触发。`halfCheckedKeys` 和 `halfCheckedNodes` 从 `2.19.0` 开始支持。|checkedKeys: `Array<string \| number>`<br>data: `{ checked?: boolean; checkedNodes: TreeNodeData[]; node?: TreeNodeData; e?: Event; halfCheckedKeys: (string \| number)[]; halfCheckedNodes: TreeNodeData[]; }`|
|expand|展开/关闭|expandKeys: `Array<string \| number>`<br>data: `{ expanded?: boolean; expandNodes: TreeNodeData[]; node?: TreeNodeData; e?: Event; }`|
|drag-start|节点开始拖拽|ev: `DragEvent`<br>node: `TreeNodeData`|
|drag-end|节点结束拖拽|ev: `DragEvent`<br>node: `TreeNodeData`|
|drag-over|节点被拖拽至可释放目标|ev: `DragEvent`<br>node: `TreeNodeData`|
|drag-leave|节点离开可释放目标|ev: `DragEvent`<br>node: `TreeNodeData`|
|drop|节点在可释放目标上释放|data: `{ e: DragEvent; dragNode: TreeNodeData; dropNode: TreeNodeData; dropPosition: number; }`|
### `<tree>` 方法

|方法名|描述|参数|返回值|版本|
|---|---|---|---|:---|
|scrollIntoView|虚拟列表滚动某个元素|options: `{ index?: number; key?: number \| string; align: 'auto' \| 'top' \| 'bottom'}`|-||
|getSelectedNodes|获取选中的节点|-|TreeNodeData[]|2.19.0|
|getCheckedNodes|获取选中复选框的节点。支持传入 `checkedStrategy`，没有传则取组件的配置。|options: ` checkedStrategy?: 'all' \| 'parent' \| 'child'; includeHalfChecked?: boolean; `|TreeNodeData[]|2.19.0|
|getHalfCheckedNodes|获取复选框半选的节点|-|TreeNodeData[]|2.19.0|
|getExpandedNodes|获取展开的节点|-|TreeNodeData[]|2.19.0|
|checkAll|设置全部节点的复选框状态|checked: ` boolean `|-|2.20.0|
|checkNode|设置指定节点的复选框状态|key: ` TreeNodeKey \| TreeNodeKey[] `<br>checked: ` boolean `<br>onlyCheckLeaf: ` boolean `|-|2.20.0，onlyCheckLeaf from 2.21.0|
|selectAll|设置全部节点的选中状态|selected: ` boolean `|-|2.20.0|
|selectNode|设置指定节点的选中状态|key: ` TreeNodeKey \| TreeNodeKey[] `<br>selected: ` boolean `|-|2.20.0|
|expandAll|设置全部节点的展开状态|expanded: ` boolean `|-|2.20.0|
|expandNode|设置指定节点的展开状态|key: ` TreeNodeKey \| TreeNodeKey[] `<br>expanded: ` boolean `|-|2.20.0|
### `<tree>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|title|标题|title: `string`||
|extra|渲染额外的节点内容|-||
|drag-icon|定制 drag 图标|node: `TreeNodeData`||
|loading-icon|定制 loading 图标|-||
|switcher-icon|定制 switcher 图标|-||
|icon|定制节点图标|node: `TreeNodeData`|2.18.0|




### TreeNodeData

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|key|唯一标示|`string \| number`|`-`|
|title|该节点显示的标题|`string`|`-`|
|selectable|是否允许选中|`boolean`|`false`|
|disabled|是否禁用节点|`boolean`|`false`|
|disableCheckbox|是否禁用复选框|`boolean`|`false`|
|checkable|是否显示多选框|`boolean`|`false`|
|draggable|是否可以拖拽|`boolean`|`false`|
|isLeaf|是否是叶子节点。动态加载时有效|`boolean`|`false`|
|icon|节点的图标|`() => VNode`|`-`|
|switcherIcon|定制 switcher 图标，优先级大于 tree|`() => VNode`|`-`|
|loadingIcon|定制 loading 图标，优先级大于 tree|`() => VNode`|`-`|
|dragIcon|定制 drag 图标，优先级大于 tree|`() => VNode`|`-`|
|children|子节点|`TreeNodeData[]`|`-`|



### TreeFieldNames

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|key|指定 key 在 TreeNodeData 中的字段名|`string`|`key`|
|title|指定 title 在 TreeNodeData 中的字段名|`string`|`title`|
|disabled|指定 disabled 在 TreeNodeData 中的字段名|`string`|`disabled`|
|children|指定 children 在 TreeNodeData 中的字段名|`string`|`children`|
|isLeaf|指定 isLeaf 在 TreeNodeData 中的字段名|`string`|`isLeaf`|
|disableCheckbox|指定 disableCheckbox 在 TreeNodeData 中的字段名|`string`|`disableCheckbox`|
|checkable|指定 checkable 在 TreeNodeData 中的字段名|`string`|`checkable`|
|icon|指定 icon 在 TreeNodeData 中的字段名|`string`|`checkable`|




### VirtualListProps

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|height|可视区域高度|`number \| string`|`-`||
|threshold|开启虚拟滚动的元素数量阈值，当数据数量小于阈值时不会开启虚拟滚动。|`number`|`-`||
|isStaticItemHeight|（已废除）元素高度是否是固定的。2.34.1 版本废除，请使用 `fixedSize`|`boolean`|`false`||
|fixedSize|元素高度是否是固定的。|`boolean`|`false`|2.34.1|
|estimatedSize|元素高度不固定时的预估高度。|`number`|`-`|2.34.1|
|buffer|视口边界外提前挂载的元素数量。|`number`|`10`|2.34.1|
