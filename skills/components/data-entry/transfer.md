---
name: arco-transfer
description: Transfer 穿梭框
---

# Transfer 穿梭框

```tsx
import { Transfer } from '@arco-design/web-react';

<Transfer
  dataSource={[
    { key: '1', value: '选项一' },
    { key: '2', value: '选项二' },
    { key: '3', value: '选项三' },
  ]}
  targetKeys={['1']}
  titleTexts={['源列表', '目标列表']}
  onChange={(newTargetKeys) => setTargetKeys(newTargetKeys)}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `dataSource` | `TransferItem[]` | 数据源 |
| `targetKeys` | `string[]` | 右侧列表 key |
| `defaultTargetKeys` | `string[]` | 默认右侧 key |
| `showSearch` | `boolean` | 搜索 |
| `showFooter` | `boolean` | 底部 |
| `titleTexts` | `ReactNode[]` | 标题 |
| `oneWay` | `boolean` | 单向模式 |
| `simple` | `boolean` | 简单模式 |
| `pagination` | `boolean \| PaginationProps` | 分页 |
| `onChange` | `(newTargetKeys, direction, moveKeys) => void` | 变化回调 |
