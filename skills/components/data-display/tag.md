---
name: arco-tag
description: Tag 标签
---

# Tag 标签

```tsx
import { Tag } from '@arco-design/web-react';

<Tag>默认</Tag>
<Tag color="red">红色</Tag>
<Tag color="arcoblue">主题色</Tag>
<Tag closable onClose={() => {}}>可关闭</Tag>
<Tag checkable defaultChecked>可选中</Tag>
<Tag size="large" bordered>大号有边框</Tag>

// 预设颜色
// red, orangered, orange, gold, lime, green, cyan, blue, arcoblue, purple, pinkpurple, magenta, gray
```

## TagProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `color` | `string` | — | 颜色（预设名或自定义色值） |
| `size` | `'small' \| 'default' \| 'medium' \| 'large'` | `'default'` | 尺寸 |
| `closable` | `boolean` | — | 可关闭 |
| `checkable` | `boolean` | — | 可选中 |
| `checked` / `defaultChecked` | `boolean` | — | 选中状态 |
| `visible` / `defaultVisible` | `boolean` | — | 显示状态 |
| `bordered` | `boolean` | — | 边框 |
| `icon` | `ReactNode` | — | 图标 |
| `closeIcon` | `ReactNode` | — | 关闭图标 |
| `onClose` | `(e) => void` | — | 关闭回调 |
| `onCheck` | `(checked) => void` | — | 选中回调 |
