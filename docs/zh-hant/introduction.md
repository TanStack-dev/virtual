---
source-updated-at: '2024-11-25T13:01:52.000Z'
translation-updated-at: '2025-05-02T15:23:35.442Z'
title: 介紹
---
TanStack Virtual 是一個無頭 UI (headless UI) 工具，用於在 JS/TS、React、Vue、Svelte、Solid、Lit 和 Angular 中虛擬化長列表元素。它並非一個元件，因此不會為您提供或渲染任何標記或樣式。雖然這需要您自行處理一些標記和樣式，但您將能 100% 掌控自己的樣式、設計與實作。

## 虛擬化器 (Virtualizer)

TanStack Virtual 的核心是 `Virtualizer`。虛擬化器 (Virtualizer) 可以設定為垂直（預設）或水平軸向，這使得結合兩種軸向配置，可以實現垂直、水平甚至網格狀的虛擬化。

以下是一個快速範例，展示如何在 React 中使用 TanStack Virtual 虛擬化一個長列表：

```tsx
import { useVirtualizer } from '@tanstack/react-virtual';

function App() {
  // 列表的可滾動元素
  const parentRef = React.useRef(null)

  // 虛擬化器 (Virtualizer)
  const rowVirtualizer = useVirtualizer({
    count: 10000,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 35,
  })

  return (
    <>
      {/* 列表的可滾動元素 */}
      <div
        ref={parentRef}
        style={{
          height: `400px`,
          overflow: 'auto', // 讓它可以滾動！
        }}
      >
        {/* 用來容納所有項目的內部大型元素 */}
        <div
          style={{
            height: `${rowVirtualizer.getTotalSize()}px`,
            width: '100%',
            position: 'relative',
          }}
        >
          {/* 僅顯示虛擬化器中可見的項目，手動定位使其出現在視野中 */}
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
              Row {virtualItem.index}
            </div>
          ))}
        </div>
      </div>
    </>
  )
}
```

讓我們深入探討更多範例！
