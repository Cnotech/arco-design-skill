---
name: arco-color-picker
description: ColorPicker 颜色选择器
---

# ColorPicker 颜色选择器

```tsx
import { ColorPicker } from '@arco-design/web-react';

<ColorPicker defaultValue="#165DFF" />
<ColorPicker showHistory showPreset />
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` | `string` | 受控颜色值 |
| `defaultValue` | `string` | 默认颜色 |
| `format` | `'hex' \| 'rgb'` | 颜色格式 |
| `showHistory` | `boolean` | 显示历史颜色 |
| `showPreset` | `boolean` | 显示预设颜色 |
| `showText` | `boolean` | 显示颜色文字 |
| `disabled` | `boolean` | 禁用 |
| `disabledAlpha` | `boolean` | 禁用透明度 |
| `onChange` | `(value: string) => void` | 变化回调 |
