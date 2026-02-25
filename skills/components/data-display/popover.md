---
name: arco-popover
description: 点击/悬停弹出气泡式卡片，可放置更复杂的内容。
---

# Popover 气泡卡片

点击/悬停弹出气泡式卡片，可放置更复杂的内容。

```tsx
import { Popover, Button } from '@arco-design/web-react';

<Popover title="标题" content="气泡卡片内容">
  <Button>悬停弹出</Button>
</Popover>

<Popover trigger="click" title="操作" content={
  <div>
    <Button type="primary" size="small">确认</Button>
  </div>
}>
  <Button>点击弹出</Button>
</Popover>
```

## PopoverProps

继承 Tooltip 的所有 props，额外支持：

| 属性 | 类型 | 说明 |
|------|------|------|
| `title` | `ReactNode` | 标题 |
| `content` | `ReactNode \| (() => ReactNode)` | 内容 |
| `position` | `'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'` | 弹出位置 |
| `trigger` | `'hover' \| 'focus' \| 'click'` | 触发方式 |
| `popupVisible` / `defaultPopupVisible` | `boolean` | 可见状态 |
| `disabled` | `boolean` | 禁用 |
| `getPopupContainer` | `(node) => Element` | 弹出容器 |
| `onVisibleChange` | `(visible: boolean) => void` | 可见变化 |
