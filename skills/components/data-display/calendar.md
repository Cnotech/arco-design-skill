---
name: arco-calendar
description: Calendar 日历
---

# Calendar 日历

```tsx
import { Calendar } from '@arco-design/web-react';

<Calendar />
<Calendar panel defaultValue="2024-01-01" />  {/* 面板模式 */}
<Calendar mode="year" />                       {/* 年视图 */}
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` / `defaultValue` | `Dayjs` | 当前日期 |
| `mode` | `'month' \| 'year'` | 视图模式 |
| `panel` | `boolean` | 面板模式（无切换按钮） |
| `panelWidth` | `number` | 面板宽度 |
| `dayStartOfWeek` | `0 \| 1` | 周起始日 |
| `dateRender` | `(date) => ReactNode` | 自定义日期渲染 |
| `dateInnerContent` | `(date) => ReactNode` | 日期内容 |
| `disabledDate` | `(date) => boolean` | 禁用日期 |
| `onChange` | `(date) => void` | 日期变化 |
| `onPanelChange` | `(date) => void` | 面板变化 |
