---
name: arco-pagination
description: Pagination 分页
---

# Pagination 分页

```tsx
import { Pagination } from '@arco-design/web-react';

<Pagination total={200} />
<Pagination total={200} showTotal showJumper showPageSize sizeCanChange />
<Pagination total={200} size="small" simple />
```

## PaginationProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `total` | `number` | — | 总条数 |
| `current` / `defaultCurrent` | `number` | `1` | 当前页 |
| `pageSize` / `defaultPageSize` | `number` | `10` | 每页条数 |
| `pageSizeChangeResetCurrent` | `boolean` | `true` | 改变每页条数时重置到第一页 |
| `showTotal` | `boolean \| ((total, range) => ReactNode)` | — | 显示总数 |
| `showJumper` | `boolean` | — | 快速跳转 |
| `showMore` | `boolean` | — | 显示更多 |
| `sizeCanChange` | `boolean` | `true` | 可改变每页条数 |
| `sizeOptions` | `number[]` | `[10,20,30,40,50]` | 每页条数选项 |
| `simple` | `boolean` | — | 简洁模式 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `disabled` | `boolean` | — | 禁用 |
| `hideOnSinglePage` | `boolean` | — | 单页隐藏 |
| `itemRender` | `(page, type, originElement) => ReactNode` | — | 自定义页码 |
| `onChange` | `(pageNumber, pageSize) => void` | — | 页码变化 |
| `onPageSizeChange` | `(size, current) => void` | — | 每页条数变化 |
