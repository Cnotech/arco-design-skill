---
name: arco-input-tag
description: 输入并管理标签列表。
---

# InputTag 标签输入

输入并管理标签列表。

```tsx
import { InputTag } from '@arco-design/web-react';

<InputTag
  allowClear
  placeholder="输入后按回车添加标签"
  defaultValue={['标签1', '标签2']}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` | `string[]` | 受控值 |
| `defaultValue` | `string[]` | 默认值 |
| `allowClear` | `boolean` | 可清除 |
| `placeholder` | `string` | 占位文字 |
| `maxTagCount` | `number` | 最多显示标签数 |
| `validate` | `(value, values) => boolean \| Promise` | 标签校验 |
| `onChange` | `(value: string[]) => void` | 变化回调 |
| `onRemove` | `(value: string, index: number) => void` | 删除标签 |
| `onPressEnter` | `(e: Event) => void` | 回车回调 |
