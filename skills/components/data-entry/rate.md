---
name: arco-rate
description: Rate 评分
---

# Rate 评分

```tsx
import { Rate } from '@arco-design/web-react';

<Rate defaultValue={3} />
<Rate allowHalf defaultValue={2.5} />
<Rate count={10} />
<Rate character={<IconHeart />} />
<Rate readonly defaultValue={4} />
```

## RateProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number` | — | 受控值 |
| `defaultValue` | `number` | — | 默认值 |
| `count` | `number` | `5` | 总数 |
| `allowHalf` | `boolean` | — | 允许半选 |
| `allowClear` | `boolean` | — | 允许清零 |
| `readonly` | `boolean` | — | 只读 |
| `disabled` | `boolean` | — | 禁用 |
| `grading` | `boolean` | — | 笑脸分级 |
| `character` | `ReactNode \| ((index: number) => ReactNode)` | — | 自定义图标 |
| `tooltips` | `string[]` | — | 各分值提示文案 |
| `onChange` | `(value: number) => void` | — | 变化回调 |
| `onHoverChange` | `(value: number) => void` | — | hover 变化 |
