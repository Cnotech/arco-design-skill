---
name: arco-steps
description: Steps 步骤条
---

# Steps 步骤条

```tsx
import { Steps } from '@arco-design/web-react';

<Steps current={2}>
  <Steps.Step title="提交" description="提交申请" />
  <Steps.Step title="审核" description="等待审核" />
  <Steps.Step title="完成" description="审核通过" />
</Steps>

// 垂直
<Steps direction="vertical" current={1}>...</Steps>

// 点状
<Steps type="dot" current={2}>...</Steps>

// 导航类型
<Steps type="navigation" current={1}>...</Steps>
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `current` | `number` | `1` | 当前步骤 |
| `type` | `'default' \| 'arrow' \| 'dot' \| 'navigation'` | `'default'` | 类型 |
| `size` | `'default' \| 'small'` | `'default'` | 尺寸 |
| `direction` | `'vertical' \| 'horizontal'` | `'horizontal'` | 方向 |
| `status` | `'wait' \| 'process' \| 'finish' \| 'error'` | — | 当前步骤状态 |
| `lineless` | `boolean` | — | 无连接线 |
| `onChange` | `(current, id) => void` | — | 点击步骤 |
