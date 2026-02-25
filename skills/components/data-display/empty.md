---
name: arco-empty
description: 当数据为空时的占位展示。
---

# Empty 空状态

当数据为空时的占位展示。

```tsx
import { Empty } from '@arco-design/web-react';

<Empty />
<Empty description="暂无数据" />
<Empty icon={<IconFile />} description="没有文件" />
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `icon` | `ReactNode` | 自定义图标 |
| `description` | `ReactNode` | 描述文字 |
| `imgSrc` | `string` | 自定义图片地址 |
