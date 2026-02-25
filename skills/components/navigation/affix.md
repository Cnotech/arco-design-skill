---
name: arco-affix
description: Affix 固钉
---

# Affix 固钉

```tsx
import { Affix, Button } from '@arco-design/web-react';

<Affix offsetTop={80}>
  <Button type="primary">固定在顶部 80px</Button>
</Affix>

<Affix offsetBottom={20}>
  <Button type="primary">固定在底部 20px</Button>
</Affix>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `offsetTop` | `number` | 距顶部距离 |
| `offsetBottom` | `number` | 距底部距离 |
| `target` | `() => HTMLElement` | 滚动容器 |
| `onChange` | `(affixed: boolean) => void` | 固钉状态变化 |
