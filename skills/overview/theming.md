---
name: arco-theming
description: Arco Design 支持通过 CSS 变量和 Less 变量两种方式进行主题定制。
---

# 主题定制

Arco Design 支持通过 CSS 变量和 Less 变量两种方式进行主题定制。

## CSS 变量方式（推荐）

通过 `ConfigProvider` 的 `theme` 属性注入 CSS 变量：

```tsx
<ConfigProvider
  theme={{
    '--color-primary-6': '#165DFF',  // 主色
    '--color-success-6': '#00B42A',  // 成功色
    '--color-warning-6': '#FF7D00',  // 警告色
    '--color-danger-6': '#F53F3F',   // 危险色
    '--border-radius-small': '2px',
    '--border-radius-medium': '4px',
    '--font-size-body-1': '14px',
    '--font-size-body-2': '13px',
    '--font-size-body-3': '12px',
  }}
>
  <App />
</ConfigProvider>
```

### 常用 CSS 变量

#### 颜色体系

Arco Design 使用 1-10 色阶体系，6 号色为标准色：

| 变量 | 说明 |
|------|------|
| `--color-primary-1` ~ `--color-primary-10` | 主色色阶 |
| `--color-success-1` ~ `--color-success-10` | 成功色色阶 |
| `--color-warning-1` ~ `--color-warning-10` | 警告色色阶 |
| `--color-danger-1` ~ `--color-danger-10` | 危险色色阶 |
| `--color-link-1` ~ `--color-link-10` | 链接色色阶 |
| `--color-bg-1` ~ `--color-bg-5` | 背景色 |
| `--color-text-1` ~ `--color-text-4` | 文字色（1 最深，4 最浅） |
| `--color-border-1` ~ `--color-border-4` | 边框色 |
| `--color-fill-1` ~ `--color-fill-4` | 填充色 |

#### 尺寸与圆角

| 变量 | 说明 |
|------|------|
| `--border-radius-none` | 0px |
| `--border-radius-small` | 2px |
| `--border-radius-medium` | 4px |
| `--border-radius-large` | 8px |
| `--border-radius-circle` | 50% |

#### 字体

| 变量 | 说明 |
|------|------|
| `--font-size-display-1` ~ `--font-size-display-3` | 展示字号 |
| `--font-size-title-1` ~ `--font-size-title-3` | 标题字号 |
| `--font-size-body-1` ~ `--font-size-body-3` | 正文字号 |
| `--font-size-caption` | 辅助字号 |

## Less 变量方式

如果使用 Less，可以在构建工具中覆盖变量：

```less
// custom-theme.less
@arcoblue-6: #165DFF;  // 主色
@green-6: #00B42A;     // 成功色
@gold-6: #FF7D00;      // 警告色
@red-6: #F53F3F;       // 危险色

@border-radius-small: 2px;
@border-radius-medium: 4px;

@font-size-body-1: 14px;
```

### Webpack 配置

```js
// webpack.config.js
module.exports = {
  module: {
    rules: [{
      test: /\.less$/,
      use: [{
        loader: 'less-loader',
        options: {
          lessOptions: {
            modifyVars: {
              'arcoblue-6': '#165DFF',
            },
            javascriptEnabled: true,
          },
        },
      }],
    }],
  },
};
```

## 暗色模式

### 方式一：引入暗色 CSS

```tsx
// 替换默认 CSS
import '@arco-design/web-react/dist/css/arco.dark.css';
```

### 方式二：通过 body 属性切换

```tsx
// 动态切换
document.body.setAttribute('arco-theme', 'dark');

// 切回亮色
document.body.removeAttribute('arco-theme');
```

### 响应系统暗色模式

```tsx
import { useEffect, useState } from 'react';

function useTheme() {
  const [dark, setDark] = useState(false);

  useEffect(() => {
    const media = window.matchMedia('(prefers-color-scheme: dark)');
    setDark(media.matches);
    const handler = (e) => setDark(e.matches);
    media.addEventListener('change', handler);
    return () => media.removeEventListener('change', handler);
  }, []);

  useEffect(() => {
    if (dark) {
      document.body.setAttribute('arco-theme', 'dark');
    } else {
      document.body.removeAttribute('arco-theme');
    }
  }, [dark]);

  return { dark, setDark };
}
```

## CSS 前缀定制

当页面中存在多套 Arco Design 或与其他库冲突时，可自定义前缀：

```tsx
<ConfigProvider prefixCls="my-app">
  <Button>自定义前缀</Button>
</ConfigProvider>
```

生成的类名将从 `arco-btn` 变为 `my-app-btn`。

同时需要配合 Less 变量：

```less
@prefix: my-app;
```

## 最佳实践

1. **优先使用 CSS 变量方式**，运行时切换无需重新编译
2. **暗色模式使用 `arco-theme` 属性方案**，方便动态切换
3. **只覆盖需要修改的变量**，其余继承默认值
4. **在设计系统中统一色阶**，使用 Arco 的 `@arco-design/color` 工具生成调色板
5. **自定义 prefixCls 时注意一致性**，Less 变量和 ConfigProvider 要同步设置
