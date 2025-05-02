---
source-updated-at: '2024-11-25T13:01:52.000Z'
translation-updated-at: '2025-05-02T20:29:09.327Z'
title: イントロダクション
---
TanStack Virtualは、JS/TS、React、Vue、Svelte、Solid、Lit、Angular向けのヘッドレスUIユーティリティで、長い要素リストの仮想化を実現します。これはコンポーネントではないため、マークアップやスタイルを提供・レンダリングすることはありません。このため、マークアップとスタイルをある程度自身で実装する必要がありますが、スタイル・デザイン・実装を100%コントロールできるという利点があります。

## バーチャライザー (Virtualizer)

TanStack Virtualの中核となるのが`Virtualizer`です。バーチャライザーは垂直（デフォルト）または水平軸に沿って設定可能で、2つの軸設定を組み合わせることで、垂直・水平方向の仮想化やグリッド状の仮想化も実現できます。

以下は、ReactでTanStack Virtualを使用して長いリストをdiv内で仮想化する簡単な例です:

```tsx
import { useVirtualizer } from '@tanstack/react-virtual';

function App() {
  // リストのスクロール可能な要素
  const parentRef = React.useRef(null)

  // バーチャライザー
  const rowVirtualizer = useVirtualizer({
    count: 10000,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 35,
  })

  return (
    <>
      {/* リストのスクロール可能な要素 */}
      <div
        ref={parentRef}
        style={{
          height: `400px`,
          overflow: 'auto', // スクロール可能に！
        }}
      >
        {/* すべてのアイテムを保持する大きな内部要素 */}
        <div
          style={{
            height: `${rowVirtualizer.getTotalSize()}px`,
            width: '100%',
            position: 'relative',
          }}
        >
          {/* バーチャライザー内で表示されるアイテムのみ、ビュー内に手動で配置 */}
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

さらにいくつかの例を見ていきましょう！
