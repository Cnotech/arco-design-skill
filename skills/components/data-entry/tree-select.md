---
name: arco-tree-select
description: TreeSelect 树选择
---

# TreeSelect 树选择

```tsx
import { TreeSelect } from '@arco-design/web-react';

<TreeSelect
  treeData={[
    {
      key: 'node1', title: '节点1',
      children: [
        { key: 'node1-1', title: '节点1-1' },
        { key: 'node1-2', title: '节点1-2' },
      ],
    },
    { key: 'node2', title: '节点2' },
  ]}
  placeholder="请选择"
  style={{ width: 300 }}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `treeData` | `TreeNodeData[]` | 树数据 |
| `value` / `defaultValue` | `string \| string[]` | 选中值 |
| `multiple` | `boolean` | 多选 |
| `treeCheckable` | `boolean` | 复选框模式 |
| `treeCheckStrictly` | `boolean` | 严格父子无关 |
| `showSearch` | `boolean` | 搜索 |
| `allowClear` | `boolean` | 可清除 |
| `loadMore` | `(node) => Promise` | 动态加载 |
| `fieldNames` | `{ key, title, children }` | 字段映射 |
| `onChange` | `(value) => void` | 变化回调 |
