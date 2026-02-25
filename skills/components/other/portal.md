---
name: arco-portal
description: 将子节点渲染到指定 DOM 节点。
---

# Portal 传送门

将子节点渲染到指定 DOM 节点。

```tsx
import { Portal } from '@arco-design/web-react';

<Portal getContainer={() => document.getElementById('target')}>
  <div>被传送的内容</div>
</Portal>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `getContainer` | `() => Element` | 目标容器 |
