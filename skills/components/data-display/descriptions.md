---
name: arco-descriptions
description: Descriptions 描述列表
---

# Descriptions 描述列表

```tsx
import { Descriptions } from '@arco-design/web-react';

<Descriptions
  title="用户信息"
  data={[
    { label: '姓名', value: '张三' },
    { label: '手机号', value: '188****8888' },
    { label: '住址', value: '北京市朝阳区' },
    { label: '备注', value: '无' },
  ]}
  column={2}
/>
```

## DescriptionsProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `data` | `{ label, value, span? }[]` | — | 描述数据 |
| `title` | `ReactNode` | — | 标题 |
| `column` | `number \| ResponsiveValue` | `3` | 每行列数 |
| `layout` | `'horizontal' \| 'vertical' \| 'inline-horizontal' \| 'inline-vertical'` | `'horizontal'` | 布局 |
| `size` | `'mini' \| 'small' \| 'medium' \| 'default' \| 'large'` | — | 尺寸 |
| `border` | `boolean` | — | 边框 |
| `colon` | `ReactNode` | — | 冒号 |
| `labelStyle` / `valueStyle` | `CSSProperties` | — | 标签/值样式 |
