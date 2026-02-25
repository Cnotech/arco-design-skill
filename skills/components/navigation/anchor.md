---
name: arco-anchor
description: Anchor 锚点
---

# Anchor 锚点

```tsx
import { Anchor } from '@arco-design/web-react';

<Anchor>
  <Anchor.Link href="#section1" title="章节一" />
  <Anchor.Link href="#section2" title="章节二">
    <Anchor.Link href="#section2-1" title="子章节" />
  </Anchor.Link>
  <Anchor.Link href="#section3" title="章节三" />
</Anchor>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `affix` | `boolean` | 是否固定 |
| `offsetTop` | `number` | 固定偏移 |
| `boundary` | `number \| 'start' \| 'center' \| 'end' \| 'nearest'` | 滚动边界 |
| `lineless` | `boolean` | 无左侧线 |
| `scrollContainer` | `string \| HTMLElement \| Window` | 滚动容器 |
| `onChange` | `(newLink, oldLink) => void` | 锚点变化 |
