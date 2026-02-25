---
name: arco-carousel
description: Carousel 走马灯
---

# Carousel 走马灯

```tsx
import { Carousel } from '@arco-design/web-react';

<Carousel autoPlay style={{ width: 600, height: 300 }}>
  <div><img src="/1.jpg" /></div>
  <div><img src="/2.jpg" /></div>
  <div><img src="/3.jpg" /></div>
</Carousel>
```

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `currentIndex` / `defaultCurrentIndex` | `number` | `0` | 当前页 |
| `autoPlay` | `boolean \| { interval, hoverToPause }` | — | 自动播放 |
| `animation` | `'slide' \| 'card' \| 'fade'` | `'slide'` | 切换动画 |
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | 方向 |
| `showArrow` | `'always' \| 'hover' \| 'never'` | `'always'` | 箭头 |
| `indicatorType` | `'line' \| 'dot' \| 'slider' \| 'never'` | `'dot'` | 指示器 |
| `indicatorPosition` | `'bottom' \| 'top' \| 'left' \| 'right' \| 'outer'` | — | 指示器位置 |
| `miniRender` | `boolean` | — | 最小化渲染（仅渲染可见） |
| `onChange` | `(index, prevIndex) => void` | — | 切换回调 |


