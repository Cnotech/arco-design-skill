---
name: arco-alert
description: 页面内的警告信息展示。
---

# Alert 警告提示

页面内的警告信息展示。

```tsx
import { Alert } from '@arco-design/web-react';

<Alert type="info" content="信息提示" />
<Alert type="success" content="成功提示" />
<Alert type="warning" content="警告提示" />
<Alert type="error" content="错误提示" />
<Alert type="info" title="标题" content="带标题的提示" closable />
<Alert banner type="warning" content="横幅式警告，适用于页面顶部" />
```

### AlertProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `'info' \| 'success' \| 'warning' \| 'error'` | `'info'` | 类型 |
| `title` | `ReactNode` | — | 标题 |
| `content` | `ReactNode` | — | 内容 |
| `showIcon` | `boolean` | `true` | 显示图标 |
| `icon` | `ReactNode` | — | 自定义图标 |
| `closable` | `boolean` | — | 可关闭 |
| `closeElement` | `ReactNode` | — | 自定义关闭元素 |
| `banner` | `boolean` | — | 横幅模式 |
| `action` | `ReactNode` | — | 操作区域 |
| `onClose` | `(e) => void` | — | 关闭回调 |
| `afterClose` | `() => void` | — | 关闭动画结束后 |


