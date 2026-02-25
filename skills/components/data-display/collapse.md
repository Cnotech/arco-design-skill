---
name: arco-collapse
description: Collapse 折叠面板
---

# Collapse 折叠面板

```tsx
import { Collapse } from '@arco-design/web-react';

<Collapse defaultActiveKey={['1']}>
  <Collapse.Item header="面板1" name="1">内容1</Collapse.Item>
  <Collapse.Item header="面板2" name="2">内容2</Collapse.Item>
  <Collapse.Item header="面板3" name="3" disabled>内容3</Collapse.Item>
</Collapse>

// 手风琴模式（同时只展开一个）
<Collapse accordion>
  <Collapse.Item header="面板1" name="1">内容1</Collapse.Item>
  <Collapse.Item header="面板2" name="2">内容2</Collapse.Item>
</Collapse>
```

## CollapseProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `activeKey` / `defaultActiveKey` | `string[]` | — | 展开的面板 |
| `accordion` | `boolean` | — | 手风琴模式 |
| `bordered` | `boolean` | `true` | 边框 |
| `expandIconPosition` | `'left' \| 'right'` | `'left'` | 展开图标位置 |
| `lazyload` | `boolean` | `true` | 延迟渲染 |
| `destroyOnHide` | `boolean` | — | 隐藏时销毁 |
| `onChange` | `(key, keys, e) => void` | — | 展开变化 |
