---
name: arco-skeleton
description: Skeleton 骨架屏
---

# Skeleton 骨架屏

```tsx
import { Skeleton } from '@arco-design/web-react';

<Skeleton loading={loading} animation>
  <div>实际内容</div>
</Skeleton>

// 自定义组合
<Skeleton loading={loading} animation text={{ rows: 3 }} image />

// 细粒度控制
<Skeleton>
  <Skeleton.Image style={{ width: 200, height: 200 }} />
  <Skeleton.Line rows={3} />
</Skeleton>
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `loading` | `boolean` | `true` | 是否显示骨架 |
| `animation` | `boolean` | — | 动画效果 |
| `image` | `boolean \| SkeletonImageProps` | — | 图片占位 |
| `text` | `boolean \| { rows, width }` | `true` | 文字占位 |

## 最佳实践

- **用于首屏加载**，给出内容布局预期
- **配合 `animation`** 提供更好的加载体验
- **组合使用 Skeleton.Image + Skeleton.Line** 模拟具体布局
