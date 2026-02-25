---
name: arco-time-picker
description: 选择时间的组件。
---

# TimePicker 时间选择器

选择时间的组件。

## 基本用法

```tsx
import { TimePicker } from '@arco-design/web-react';

<TimePicker style={{ width: 200 }} />
<TimePicker format="HH:mm" style={{ width: 150 }} />
<TimePicker.RangePicker style={{ width: 280 }} />
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `Dayjs \| string` | — | 受控值 |
| `defaultValue` | `Dayjs \| string` | — | 默认值 |
| `format` | `string` | `'HH:mm:ss'` | 时间格式 |
| `use12Hours` | `boolean` | — | 12 小时制 |
| `step` | `{ hour, minute, second }` | — | 各列步长 |
| `disableConfirm` | `boolean` | — | 选择即确认 |
| `disabled` | `boolean` | — | 禁用 |
| `allowClear` | `boolean` | `true` | 可清除 |
| `placeholder` | `string` | — | 占位文字 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `showNowBtn` | `boolean` | `true` | 显示"此刻"按钮 |
| `onChange` | `(timeString, time) => void` | — | 值变化 |


