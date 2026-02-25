---
name: arco-divider
description: 区隔内容的分割线，支持水平和垂直方向。
---

# Divider 分割线

区隔内容的分割线，支持水平和垂直方向。

```tsx
import { Divider } from '@arco-design/web-react';

// 水平分割线
<Divider />

// 带文字
<Divider>居中文字</Divider>
<Divider orientation="left">左侧文字</Divider>
<Divider orientation="right">右侧文字</Divider>

// 垂直分割线
<span>文本</span>
<Divider type="vertical" />
<span>文本</span>

// 虚线
<Divider style={{ borderBottomStyle: 'dashed' }} />
```

## DividerProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `'horizontal' \| 'vertical'` | `'horizontal'` | 方向 |
| `orientation` | `'left' \| 'center' \| 'right'` | `'center'` | 文字位置 |
