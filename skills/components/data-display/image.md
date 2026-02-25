---
name: arco-image
description: Image 图片
---

# Image 图片

```tsx
import { Image } from '@arco-design/web-react';

<Image src="/photo.jpg" width={200} alt="photo" />

// 图片组（支持预览切换）
<Image.PreviewGroup>
  <Image src="/1.jpg" width={200} />
  <Image src="/2.jpg" width={200} />
  <Image src="/3.jpg" width={200} />
</Image.PreviewGroup>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `src` | `string` | 图片地址 |
| `width` / `height` | `number \| string` | 尺寸 |
| `title` / `description` | `string` | 标题/描述 |
| `preview` | `boolean` | 可预览（默认 true） |
| `previewProps` | `ImagePreviewProps` | 预览配置 |
| `error` | `ReactNode` | 加载失败内容 |
| `loader` | `boolean \| ReactNode` | 加载中 |
| `lazyload` | `boolean \| IntersectionObserverInit` | 懒加载 |
| `footerPosition` | `'inner' \| 'outer'` | 底部信息位置 |
| `actions` | `ReactNode[]` | 预览操作 |
