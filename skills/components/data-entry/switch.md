---
name: arco-switch
description: Switch 开关
---

# Switch 开关

```tsx
import { Switch } from '@arco-design/web-react';

<Switch />
<Switch defaultChecked />
<Switch type="round" />  {/* 圆形 */}
<Switch type="line" />   {/* 线性 */}
<Switch checkedText="ON" uncheckedText="OFF" />
<Switch loading />
```

### SwitchProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `checked` | `boolean` | — | 受控选中 |
| `defaultChecked` | `boolean` | — | 默认选中 |
| `type` | `'circle' \| 'round' \| 'line'` | `'circle'` | 类型 |
| `size` | `'small' \| 'default'` | `'default'` | 尺寸 |
| `loading` | `boolean` | — | 加载中 |
| `disabled` | `boolean` | — | 禁用 |
| `checkedText` | `ReactNode` | — | 选中时文字 |
| `uncheckedText` | `ReactNode` | — | 未选中时文字 |
| `checkedIcon` | `ReactNode` | — | 选中时图标 |
| `uncheckedIcon` | `ReactNode` | — | 未选中时图标 |
| `onChange` | `(value: boolean, e: Event) => void` | — | 变化回调 |

> **在 Form 中使用**：设置 `<Form.Item triggerPropName="checked">` 因为 Switch 使用 `checked` 而非 `value`。


