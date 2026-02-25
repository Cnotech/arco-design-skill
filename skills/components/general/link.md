---
name: arco-link
description: 基础超链接组件，支持不同状态和图标。
---

# Link 链接

基础超链接组件，支持不同状态和图标。

```tsx
import { Link } from '@arco-design/web-react';

<Link href="https://arco.design">默认链接</Link>
<Link href="/page" status="success">成功链接</Link>
<Link href="/page" status="warning">警告链接</Link>
<Link href="/page" status="danger">危险链接</Link>
<Link disabled>禁用链接</Link>
<Link icon>带图标的链接</Link>  {/* 自动添加外链图标 */}
```

### LinkProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `href` | `string` | — | 链接地址 |
| `status` | `'success' \| 'warning' \| 'danger' \| 'default'` | `'default'` | 链接状态 |
| `disabled` | `boolean` | — | 禁用 |
| `icon` | `boolean \| ReactNode` | — | 显示图标 |
| `hoverable` | `boolean` | `true` | 是否有 hover 下划线 |


