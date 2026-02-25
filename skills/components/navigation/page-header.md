---
name: arco-page-header
description: PageHeader 页头
---

# PageHeader 页头

```tsx
import { PageHeader, Button } from '@arco-design/web-react';

<PageHeader
  title="页面标题"
  subTitle="副标题"
  breadcrumb={{
    routes: [
      { path: '/', breadcrumbName: '首页' },
      { path: '/list', breadcrumbName: '列表' },
      { breadcrumbName: '详情' },
    ],
  }}
  extra={<Button type="primary">操作</Button>}
>
  页面内容描述
</PageHeader>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `title` | `ReactNode` | 标题 |
| `subTitle` | `ReactNode` | 副标题 |
| `breadcrumb` | `BreadcrumbProps` | 面包屑配置 |
| `extra` | `ReactNode` | 右侧操作区 |
| `backIcon` | `ReactNode \| boolean` | 返回图标 |
| `onBack` | `(e) => void` | 返回回调 |
| `footer` | `ReactNode` | 底部内容 |
