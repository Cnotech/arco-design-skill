---
name: arco-back-top
description: BackTop 回到顶部
---

# BackTop 回到顶部

```tsx
import { BackTop } from '@arco-design/web-react';

<BackTop />
<BackTop visibleHeight={200} duration={500} />

// 自定义
<BackTop>
  <div style={{ width: 40, height: 40, background: '#165DFF', borderRadius: '50%', display: 'flex', alignItems: 'center', justifyContent: 'center', color: '#fff' }}>
    UP
  </div>
</BackTop>
```

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `visibleHeight` | `number` | `400` | 出现的滚动高度 |
| `target` | `() => HTMLElement` | `() => window` | 滚动容器 |
| `duration` | `number` | `400` | 滚动时长 ms |
| `onClick` | `() => void` | — | 点击回调 |


