---
name: arco-slider
description: Slider 滑动输入条
---

# Slider 滑动输入条

```tsx
import { Slider } from '@arco-design/web-react';

<Slider defaultValue={30} />
<Slider range defaultValue={[20, 60]} />
<Slider marks={{ 0: '0°C', 25: '25°C', 50: '50°C', 100: '100°C' }} />
<Slider step={10} showTicks />
<Slider vertical style={{ height: 200 }} />
```

## SliderProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number \| [number, number]` | — | 受控值 |
| `defaultValue` | `number \| [number, number]` | — | 默认值 |
| `min` | `number` | `0` | 最小值 |
| `max` | `number` | `100` | 最大值 |
| `step` | `number` | `1` | 步长 |
| `range` | `boolean` | — | 范围选择 |
| `vertical` | `boolean` | — | 垂直方向 |
| `marks` | `Record<number, ReactNode>` | — | 刻度标记 |
| `showTicks` | `boolean` | — | 显示刻度 |
| `showInput` | `boolean` | — | 显示输入框 |
| `disabled` | `boolean` | — | 禁用 |
| `reverse` | `boolean` | — | 反向 |
| `tooltipVisible` | `boolean` | — | 提示是否一直显示 |
| `formatTooltip` | `(value: number) => ReactNode` | — | 提示格式化 |
| `onChange` | `(value) => void` | — | 值变化（松开后） |
| `onAfterChange` | `(value) => void` | — | 拖拽结束回调 |
