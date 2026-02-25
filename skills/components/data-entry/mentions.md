---
name: arco-mentions
description: Mentions 提及
---

# Mentions 提及

```tsx
import { Mentions } from '@arco-design/web-react';

<Mentions
  options={['张三', '李四', '王五'].map(name => ({ value: name, label: name }))}
  placeholder="输入 @ 提及用户"
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `prefix` | `string \| string[]` | 触发字符（默认 `@`） |
| `options` | `{ value, label }[]` | 提及选项 |
| `split` | `string` | 分隔符 |
| `onSearch` | `(text, prefix) => void` | 搜索回调 |
| `onChange` | `(value) => void` | 值变化 |
