---
name: arco-badge
description: Badge 徽标
---

# Badge 徽标

```tsx
import { Badge, Avatar } from '@arco-design/web-react';

<Badge count={5}><Avatar shape="square">头像</Avatar></Badge>
<Badge count={100} maxCount={99}><Avatar shape="square">头像</Avatar></Badge>
<Badge dot><Avatar shape="square">头像</Avatar></Badge>
<Badge status="processing" text="进行中" />
<Badge color="#165DFF" text="自定义颜色" />
```

## BadgeProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `count` | `number \| ReactNode` | — | 数字 |
| `maxCount` | `number` | `99` | 最大显示数 |
| `dot` | `boolean` | — | 小红点 |
| `dotStyle` | `CSSProperties` | — | 点样式 |
| `offset` | `[number, number]` | — | 偏移 |
| `text` | `string` | — | 文本 |
| `status` | `'default' \| 'processing' \| 'success' \| 'warning' \| 'error'` | — | 状态点 |
| `color` | `string` | — | 自定义颜色 |
