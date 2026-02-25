---
name: arco-verification-code
description: VerificationCode 验证码
---

# VerificationCode 验证码

```tsx
import { VerificationCode } from '@arco-design/web-react';

<VerificationCode length={6} onChange={(value) => console.log(value)} />
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `length` | `number` | 验证码位数 |
| `value` / `defaultValue` | `string` | 值 |
| `separator` | `(data: { index, character }) => ReactNode` | 分隔符 |
| `disabled` | `boolean` | 禁用 |
| `masked` | `boolean` | 掩码显示 |
| `onChange` | `(value: string) => void` | 变化回调 |
| `onFinish` | `(value: string) => void` | 输入完成 |
