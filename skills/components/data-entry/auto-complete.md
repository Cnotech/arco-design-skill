---
name: arco-auto-complete
description: 输入框自动补全组件。
---

# AutoComplete 自动补全

输入框自动补全组件。

```tsx
import { AutoComplete } from '@arco-design/web-react';

<AutoComplete
  placeholder="请输入"
  data={['北京', '上海', '广州', '深圳']}
  style={{ width: 300 }}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `data` | `(string \| { value, name })[]` | 数据源 |
| `filterOption` | `boolean \| (inputValue, option) => boolean` | 过滤函数 |
| `triggerElement` | `ReactNode` | 自定义触发元素 |
| `onSearch` | `(value: string) => void` | 搜索回调 |
| `onSelect` | `(value: string) => void` | 选中回调 |
| `virtualListProps` | `object` | 虚拟滚动 |
