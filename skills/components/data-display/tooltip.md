---
name: arco-tooltip
description: 简单的文字提示气泡框。
---

# Tooltip 文字气泡

简单的文字提示气泡框。

```tsx
import { Tooltip, Button } from '@arco-design/web-react';

<Tooltip content="提示文字">
  <Button>鼠标悬停</Button>
</Tooltip>

<Tooltip position="right" content="右侧提示" color="#165DFF">
  <Button>右侧</Button>
</Tooltip>
```

### TooltipProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `content` | `ReactNode` | — | 提示内容 |
| `position` | `'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'` | `'top'` | 弹出位置 |
| `trigger` | `'hover' \| 'focus' \| 'click'` | `'hover'` | 触发方式 |
| `popupVisible` | `boolean` | — | 受控可见 |
| `defaultPopupVisible` | `boolean` | — | 默认可见 |
| `color` | `string` | — | 背景色 |
| `mini` | `boolean` | — | 迷你模式 |
| `disabled` | `boolean` | — | 禁用 |
| `getPopupContainer` | `(node) => Element` | — | 弹出容器 |
| `onVisibleChange` | `(visible: boolean) => void` | — | 可见变化 |


