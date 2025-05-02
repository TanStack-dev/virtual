---
source-updated-at: '2024-11-25T13:01:52.000Z'
translation-updated-at: '2025-04-08T03:44:09.958Z'
title: 介绍
---
TanStack Virtual 是一个用于在 JS/TS、React、Vue、Svelte、Solid、Lit 和 Angular 中虚拟化长元素列表的无头 UI 工具 (headless UI utility)。它不是一个组件，因此不会提供或渲染任何标记或样式。虽然这需要您自行处理一些标记和样式，但您将保留对样式、设计和实现的 100% 控制权。

## 虚拟化器 (Virtualizer)

TanStack Virtual 的核心是 `Virtualizer`。虚拟化器 (virtualizer) 可以设置为垂直（默认）或水平方向，这使得通过结合两种轴向配置，可以实现垂直、水平甚至类似网格的虚拟化 (virtualization)。

以下是一个在 React 中使用 TanStack Virtual 虚拟化长列表的简单示例：

```tsx
import { useVirtualizer } from '@tanstack/react-virtual';

function App() {
  // 列表的可滚动元素 (scroll element)
  const parentRef = React.useRef(null)

  // 虚拟化器 (virtualizer)
  const rowVirtualizer = useVirtualizer({
    count: 10000,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 35,
  })

  return (
    <>
      {/* 列表的可滚动元素 (scroll element) */}
      <div
        ref={parentRef}
        style={{
          height: `400px`,
          overflow: 'auto', // 使其可滚动！
        }}
      >
        {/* 容纳所有项的大型内部元素 */}
        <div
          style={{
            height: `${rowVirtualizer.getTotalSize()}px`,
            width: '100%',
            position: 'relative',
          }}
        >
          {/* 仅虚拟化器 (virtualizer) 中可见的项，手动定位以显示在视图中 */}
          {rowVirtualizer.getVirtualItems().map((virtualItem) => (
            <div
              key={virtualItem.key}
              style={{
                position: 'absolute',
                top: 0,
                left: 0,
                width: '100%',
                height: `${virtualItem.size}px`,
                transform: `translateY(${virtualItem.start}px)`,
              }}
            >
              行 {virtualItem.index}
            </div>
          ))}
        </div>
      </div>
    </>
  )
}
```

让我们深入探讨更多示例！
