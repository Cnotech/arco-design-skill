---
name: arco-result
description: Result 结果页
---

# Result 结果页

```tsx
import { Result, Button } from '@arco-design/web-react';

<Result
  status="success"
  title="操作成功"
  subTitle="订单已提交，请等待审核。"
  extra={[
    <Button key="back" type="secondary">返回列表</Button>,
    <Button key="again" type="primary">再次提交</Button>,
  ]}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `status` | `'success' \| 'error' \| 'info' \| 'warning' \| '404' \| '403' \| '500' \| null` | 状态 |
| `title` | `ReactNode` | 标题 |
| `subTitle` | `ReactNode` | 副标题 |
| `icon` | `ReactNode` | 自定义图标 |
| `extra` | `ReactNode` | 操作区 |
