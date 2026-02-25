---
name: arco-hooks
description: Hooks 参考
---

# Hooks 参考

## 公开 Hooks

从 `@arco-design/web-react/hooks` 导入，可用于构建自定义组件。

### useVerificationCode

无头验证码输入 Hook，管理多个单字符输入框的值、焦点、粘贴和键盘导航。

```ts
import { useVerificationCode } from '@arco-design/web-react/hooks';
```

**参数 (Options)**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `length` | `number` | `6` | 验证码位数 |
| `defaultValue` | `string` | — | 非受控初始值 |
| `value` | `string` | — | 受控值 |
| `onChange` | `(value: string) => void` | — | 值变化回调 |
| `onFinish` | `(value: string) => void` | — | 所有位填满时回调 |
| `getInputRefList` | `() => HTMLInputElement[]` | — | 返回输入框 DOM 列表 |

**返回值**

| 属性 | 类型 | 说明 |
|------|------|------|
| `filledValue` | `string[]` | 每一位的值数组 |
| `value` | `string` | 当前拼接后的完整值 |
| `setValue` | `(value: string) => void` | 命令式设置值 |
| `getInputProps` | `(index: number) => InputProps` | 获取第 N 个输入框的 props |

**示例**

```tsx
import { useVerificationCode } from '@arco-design/web-react/hooks';

const CustomOTP = () => {
  const inputRefList = React.useRef<HTMLInputElement[]>([]);

  const { filledValue, getInputProps } = useVerificationCode({
    length: 6,
    getInputRefList: () => inputRefList.current || [],
    onFinish: (value) => {
      console.log('验证码:', value);
    },
  });

  return (
    <div style={{ display: 'flex', gap: 8 }}>
      {filledValue.map((v, index) => {
        const inputProps = { ...getInputProps(index) };
        return (
          <input
            key={index}
            ref={(node) => { inputRefList.current[index] = node; }}
            style={{ width: 40, height: 40, textAlign: 'center', fontSize: 18 }}
            {...inputProps}
            onChange={(e) => inputProps.onChange?.(e.target.value)}
          />
        );
      })}
    </div>
  );
};
```

---

### useWatermark

无头水印 Hook，通过 Canvas 渲染水印层，支持文字/图片、旋转、自定义字体，使用 MutationObserver 防止水印被篡改。

```ts
import { useWatermark } from '@arco-design/web-react/hooks';
```

**参数 (Options)**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `zIndex` | `number` | `1` | 水印 z-index |
| `width` | `number \| string` | `100`(图片) | 单个水印宽度 |
| `height` | `number \| string` | — | 单个水印高度 |
| `rotate` | `number` | `-20` | 旋转角度 |
| `image` | `string` | — | 图片 URL（优先级高于 content） |
| `content` | `string \| string[]` | — | 文字内容（数组支持多行） |
| `fontStyle` | `object` | — | 字体样式 |
| `gap` | `[number, number]` | `[100, 100]` | 水印间距 |
| `offset` | `[number, number]` | — | 偏移量 |
| `getContainer` | `() => HTMLElement` | — | 容器元素 |

**返回值**

| 属性 | 类型 | 说明 |
|------|------|------|
| `destroy` | `() => void` | 移除水印并清理 observer |
| `setWatermark` | `(options) => void` | 应用或更新水印 |

**示例**

```tsx
import { useWatermark } from '@arco-design/web-react/hooks';

const CustomWatermark = ({ children, content }) => {
  const containerRef = React.useRef<HTMLDivElement>(null);
  const { setWatermark, destroy } = useWatermark({});

  React.useEffect(() => {
    if (containerRef.current) {
      setWatermark({
        content,
        fontStyle: { color: 'rgba(0, 0, 0, 0.1)', fontSize: 16 },
        getContainer: () => containerRef.current!,
      });
    }
    return () => destroy();
  }, [content]);

  return (
    <div ref={containerRef} style={{ position: 'relative' }}>
      {children}
    </div>
  );
};
```

---

## 内部 Hooks（不在公开 API 中）

这些 Hook 位于 `components/_util/hooks/`，被组件内部大量使用，了解它们有助于理解组件设计和自定义开发。

### 核心状态管理

#### useMergeValue

受控/非受控值合并，几乎所有有状态组件都使用：

```ts
function useMergeValue<T>(
  defaultStateValue: T,
  props?: { defaultValue?: T; value?: T }
): [T, React.Dispatch<React.SetStateAction<T>>, T]
```

返回 `[mergedValue, setValue, stateValue]`。当 `props.value` 存在时为受控模式，否则使用内部状态。

#### useMergeProps

合并组件 props、默认值和 ConfigProvider 全局配置：

```ts
function useMergeProps<P>(
  componentProps: P,
  defaultProps: Partial<P>,
  globalComponentConfig: Partial<P>
): P
```

### 生命周期

| Hook | 说明 |
|------|------|
| `useUpdate` | state 变化时触发回调（跳过相同值） |
| `useUpdateEffect` | 同 `useEffect` 但跳过首次渲染 |
| `usePrevious` | 返回上一次渲染的值 |
| `useIsFirstRender` | 首次渲染返回 `true` |
| `useIsomorphicLayoutEffect` | 浏览器用 `useLayoutEffect`，SSR 用 `useEffect` |
| `useStateWithPromise` | `setState` 返回 Promise 等待更新完成 |

### UI 工具

| Hook | 说明 |
|------|------|
| `useOverflowHidden` | Modal/Drawer 打开时隐藏滚动条，补偿宽度防止抖动 |
| `useKeyboardEvent` | 将键盘操作（Enter、Escape 等）映射为处理函数 |
| `useForceUpdate` | 强制重新渲染 |

### 观察者

| Hook | 说明 |
|------|------|
| `useResizeObserver` | 封装 ResizeObserver |
| `useMutationObserver` | 封装 MutationObserver |
| `useElementInView` | 检测元素是否在视口中（IntersectionObserver） |

### 其他

| Hook | 说明 |
|------|------|
| `useId` | 生成唯一递增 ID，SSR 兼容 |
| `useInterval` | 管理 setInterval，自动清理 |
| `useCallbackRef` | 返回稳定的回调引用 |
| `useStateCallback` | `useState` + 更新后回调（类似 class 组件 `setState`） |
| `useComputeState` | 当依赖变化时重新计算衍生状态 |
| `useRefList` | 管理可变 ref 列表 |
| `useElementRef` | 克隆元素以拦截 ref |

---

## 架构说明

- **公开 Hooks** 独立于组件，可用于无头模式自定义 UI
- `@arco-design/web-react/hooks` 路径指向 `hooks/` 包的编译产物
- 内部 Hooks 不导出，但可以作为自定义 Hook 的参考
- 核心模式：`useMergeValue`（受控/非受控）+ `useMergeProps`（props 合并）— 几乎每个组件都依赖这两个
