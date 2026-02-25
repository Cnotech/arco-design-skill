---
name: arco-breadcrumb
description: Breadcrumb 面包屑
---

# Breadcrumb 面包屑

```tsx
import { Breadcrumb } from '@arco-design/web-react';

<Breadcrumb>
  <Breadcrumb.Item>首页</Breadcrumb.Item>
  <Breadcrumb.Item href="/list">列表</Breadcrumb.Item>
  <Breadcrumb.Item>详情</Breadcrumb.Item>
</Breadcrumb>

// 自定义分隔符
<Breadcrumb separator=">" />

// 下拉菜单
<Breadcrumb.Item droplist={<Menu><Menu.Item>选项</Menu.Item></Menu>}>
  分类
</Breadcrumb.Item>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `separator` | `ReactNode` | 自定义分隔符 |
| `maxCount` | `number` | 最多显示的面包屑数量 |
| `routes` | `{ path, breadcrumbName }[]` | 通过配置生成 |

### Breadcrumb.Item

| 属性 | 类型 | 说明 |
|------|------|------|
| `href` | `string` | 链接地址 |
| `droplist` | `ReactNode` | 下拉菜单 |
| `onClick` | `(e) => void` | 点击回调 |
