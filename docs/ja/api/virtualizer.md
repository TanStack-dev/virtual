---
source-updated-at: '2025-05-05T15:05:35.000Z'
translation-updated-at: '2025-05-06T23:02:25.839Z'
title: バーチャライザー
---
`Virtualizer` クラスは TanStack Virtual のコアです。通常、Virtualizer インスタンスはフレームワークアダプタによって作成されますが、直接 virtualizer を受け取ることもできます。

```tsx
export class Virtualizer<TScrollElement = unknown, TItemElement = unknown> {
  constructor(options: VirtualizerOptions<TScrollElement, TItemElement>)
}
```

## 必須オプション

### `count`

```tsx
count: number
```

仮想化するアイテムの総数。

### `getScrollElement`

```tsx
getScrollElement: () => TScrollElement
```

virtualizer のスクロール可能な要素を返す関数。要素がまだ利用できない場合は null を返すことがあります。

### `estimateSize`

```tsx
estimateSize: (index: number) => number
```

> 🧠 要素を動的に計測する場合、アイテムの可能な限り大きいサイズ（快適な範囲内での幅/高さ）を見積もることを推奨します。これにより、スムーズスクロールなどの機能が正しく動作する可能性が高まります。

この関数は各アイテムのインデックスを受け取り、各アイテムの実際のサイズ（または `virtualItem.measureElement` で動的に計測する場合は推定サイズ）を返す必要があります。この計測は、virtualizer の向きに応じて幅または高さを返す必要があります。

## オプション

### `enabled`

```tsx
enabled?: boolean
```

`false` に設定すると、scrollElement のオブザーバーが無効になり、virtualizer の状態がリセットされます

### `debug`

```tsx
debug?: boolean
```

`true` に設定するとデバッグログが有効になります

### `initialRect`

```tsx
initialRect?: Rect
```

scrollElement の初期 `Rect`。主に SSR 環境で virtualizer を実行する必要がある場合に有用です。それ以外の場合は、初期 Rect は `observeElementRect` の実装によってマウント時に計算されます。

### `onChange`

```tsx
onChange?: (instance: Virtualizer<TScrollElement, TItemElement>, sync: boolean) => void
```

virtualizer の内部状態が変化したときに発火するコールバック関数。virtualizer インスタンスと sync パラメータが渡されます。

sync パラメータは、スクロールが現在進行中かどうかを示します。スクロール中は `true`、スクロールが停止したときやリサイズなどの他のアクションが実行されているときは `false` になります。

### `overscan`

```tsx
overscan?: number
```

可視領域の上下にレンダリングするアイテムの数。この数を増やすと virtualizer のレンダリング時間が増加しますが、スクロール時に virtualizer の上部や下部でレンダリングが遅い空白アイテムが表示される可能性が減少します。デフォルト値は `1` です。

### `horizontal`

```tsx
horizontal?: boolean
```

virtualizer が水平方向の場合、これを `true` に設定します。

### `paddingStart`

```tsx
paddingStart?: number
```

virtualizer の開始部分に適用するパディング（ピクセル単位）。

### `paddingEnd`

```tsx
paddingEnd?: number
```

virtualizer の終了部分に適用するパディング（ピクセル単位）。

### `scrollPaddingStart`

```tsx
scrollPaddingStart?: number
```

要素にスクロールするときに virtualizer の開始部分に適用するパディング（ピクセル単位）。

### `scrollPaddingEnd`

```tsx
scrollPaddingEnd?: number
```

要素にスクロールするときに virtualizer の終了部分に適用するパディング（ピクセル単位）。

### `initialOffset`

```tsx
initialOffset?: number | (() => number)
```

virtualizer に適用する初期オフセット。通常、SSR 環境で virtualizer をレンダリングする場合にのみ有用です。

### `getItemKey`

```tsx
getItemKey?: (index: number) => Key
```

この関数は各アイテムのインデックスを受け取り、そのアイテムの一意のキーを返す必要があります。この関数のデフォルト機能はアイテムのインデックスを返すことですが、可能であればセット全体で各アイテムの一意の識別子を返すようにオーバーライドする必要があります。この関数は不要な再レンダリングを防ぐためにメモ化する必要があります。

### `rangeExtractor`

```tsx
rangeExtractor?: (range: Range) => number[]
```

この関数は可視範囲のインデックスを受け取り、レンダリングするインデックスの配列を返す必要があります。これは、可視範囲に関係なく手動でアイテムを追加または削除する必要がある場合（例: 固定アイテム、ヘッダー、フッターなどをレンダリングする場合）に有用です。デフォルトの range extractor 実装は可視範囲のインデックスを返し、`defaultRangeExtractor` としてエクスポートされます。

### `scrollToFn`

```tsx
scrollToFn?: (
  offset: number,
  options: { adjustments?: number; behavior?: 'auto' | 'smooth' },
  instance: Virtualizer<TScrollElement, TItemElement>,
) => void
```

オプションの関数で、（提供されている場合）scrollElement のスクロール動作を実装する必要があります。以下の引数で呼び出されます:

- スクロール先の `offset`（ピクセル単位）。
- 推定サイズと実際のサイズの差 (`adjustments`) やスムーズアニメーションでスクロールが呼び出されたかどうか (`behaviour`) を示すオブジェクト。
- virtualizer インスタンス自体。

組み込みのスクロール実装は `elementScroll` および `windowScroll` としてエクスポートされており、`useVirtualizer` や `useWindowVirtualizer` などのフレームワークアダプタ関数によって自動的に構成されます。

> ⚠️ 動的に計測される要素で smoothScroll を使用しようとしても動作しません。

### `observeElementRect`

```tsx
observeElementRect: (
  instance: Virtualizer<TScrollElement, TItemElement>,
  cb: (rect: Rect) => void,
) => void | (() => void)
```

オプションの関数で、（提供されている場合）scrollElement が変更されたときに呼び出され、scrollElement の `Rect`（`width` と `height` を持つオブジェクト）の初期計測と継続的な監視を実装する必要があります。インスタンス（`instance.scrollElement` を介して scrollElement にアクセス可能）とともに呼び出されます。組み込みの実装は `observeElementRect` および `observeWindowRect` としてエクスポートされており、`useVirtualizer` や `useWindowVirtualizer` などのフレームワークアダプタのエクスポート関数によって自動的に構成されます。

### `observeElementOffset`

```tsx
observeElementOffset: (
    instance: Virtualizer<TScrollElement, TItemElement>,
    cb: (offset: number) => void,
  ) => void | (() => void)
```

オプションの関数で、（提供されている場合）scrollElement が変更されたときに呼び出され、scrollElement のスクロールオフセット（数値）の初期計測と継続的な監視を実装する必要があります。インスタンス（`instance.scrollElement` を介して scrollElement にアクセス可能）とともに呼び出されます。組み込みの実装は `observeElementOffset` および `observeWindowOffset` としてエクスポートされており、`useVirtualizer` や `useWindowVirtualizer` などのフレームワークアダプタのエクスポート関数によって自動的に構成されます。

### `measureElement`

```tsx
measureElement?: (
  element: TItemElement,
  entry: ResizeObserverEntry | undefined,
  instance: Virtualizer<TScrollElement, TItemElement>,
) => number
```

このオプション関数は、virtualizer がアイテムのサイズ（幅または高さ）を動的に計測する必要があるときに呼び出されます。

> 🧠 `instance.options.horizontal` を使用して、アイテムの幅または高さを計測するかどうかを判断できます。

### `scrollMargin`

```tsx
scrollMargin?: number
```

このオプションを使用すると、スクロールオフセットの起点を指定できます。通常、この値はスクロール要素の先頭とリストの開始位置の間のスペースを表します。これは、ウィンドウ virtualizer の前にヘッダーがある一般的なシナリオや、単一のスクロール要素内で複数の virtualizer が使用されている場合に特に有用です。要素を絶対位置指定で配置する場合は、CSS トランスフォームで `scrollMargin` を考慮する必要があります:
```tsx
transform: `translateY(${
   virtualRow.start - rowVirtualizer.options.scrollMargin
}px)` 
``` 
`scrollMargin` の値を動的に計測するには、`getBoundingClientRect()` または ResizeObserver を使用できます。これは、仮想リストの上のアイテムの高さが変更される可能性があるシナリオで役立ちます。

### `gap`

```tsx
gap?: number
```

このオプションを使用すると、仮想化リスト内のアイテム間のスペースを設定できます。各アイテムのマージンやパディングを手動で調整することなく、一貫した視覚的な間隔を維持するのに特に便利です。値はピクセル単位で指定します。

### `lanes`

```tsx
lanes: number
```

リストが分割されるレーン数（垂直リストの場合は列、水平リストの場合は行）。

### `isScrollingResetDelay`

```tsx
isScrollingResetDelay: number
```

このオプションを使用すると、最後のスクロールイベントから isScrolling インスタンスプロパティをリセットするまでの待機時間を指定できます。デフォルト値は 150 ミリ秒です。

このオプションの実装は、さまざまなブラウザ間でスクロール動作を処理する信頼性の高いメカニズムの必要性によって推進されています。すべてのブラウザが scrollEnd イベントを一様にサポートするまで。

### `useScrollendEvent`

```tsx
useScrollendEvent: boolean
```

スクロールが停止したことを検出するためにネイティブの scrollend イベントを使用するかどうかを決定します。false に設定すると、isScrollingResetDelay ミリ秒後に isScrolling インスタンスプロパティをリセットするためにデバウンスされたフォールバックが使用されます。デフォルト値は `false` です。

このオプションの実装は、さまざまなブラウザ間でスクロール動作を処理する信頼性の高いメカニズムの必要性によって推進されています。すべてのブラウザが scrollEnd イベントを一様にサポートするまで。

### `isRtl`

```tsx
isRtl: boolean
```

右から左への言語ロケールをサポートするために水平スクロールを反転するかどうか。

### `useAnimationFrameWithResizeObserver`

```tsx
useAnimationFrameWithResizeObserver: boolean
```

このオプションを有効にすると、ResizeObserver の計測を requestAnimationFrame でラップし、更新をスムーズにし、レイアウトスラッシングを減らします。デフォルト値は `false` です。

これにより、計測がレンダリングサイクルに合わせられることで、"ResizeObserver loop completed with undelivered notifications" エラーを防ぐことができます。これは、特に要素を動的にリサイズする場合に、パフォーマンスを向上させ、UI のジャターを減らすことができます。ただし、ResizeObserver はすでに非同期で実行されるため、requestAnimationFrame を追加すると計測にわずかな遅延が生じ、場合によっては目立つ可能性があります。リサイズ操作が軽量でリフローを引き起こさない場合、このオプションを有効にしても大きな利点は得られない可能性があります。

## Virtualizer インスタンス

以下のプロパティとメソッドが virtualizer インスタンスで利用可能です:

### `options`

```tsx
options: readonly Required<VirtualizerOptions<TScrollElement, TItemElement>>
```

virtualizer の現在のオプション。このプロパティはフレームワークアダプタによって更新され、読み取り専用です。

### `scrollElement`

```tsx
scrollElement: readonly TScrollElement | null
```

virtualizer の現在の scrollElement。このプロパティはフレームワークアダプタによって更新され、読み取り専用です。

### `getVirtualItems`

```tsx
type getVirtualItems = () => VirtualItem[]
```

virtualizer の現在の状態に対する仮想アイテムを返します。

### `getVirtualIndexes`

```tsx
type getVirtualIndexes = () => number[]
```

virtualizer の現在の状態に対する仮想行インデックスを返します。

### `scrollToOffset`

```tsx
scrollToOffset: (
  toOffset: number,
  options?: {
    align?: 'start' | 'center' | 'end' | 'auto',
    behavior?: 'auto' | 'smooth'
  }
) => void
```

virtualizer を指定されたピクセルオフセットにスクロールします。オプションで、スクロールを scrollElement の特定の部分にアンカーするためのアラインモードを渡すことができます。

### `scrollToIndex`

```tsx
scrollToIndex: (
  index: number,
  options?: {
    align?: 'start' | 'center' | 'end' | 'auto',
    behavior?: 'auto' | 'smooth'
  }
) => void
```

virtualizer を指定されたインデックスのアイテムにスクロールします。オプションで、スクロールを scrollElement の特定の部分にアンカーするためのアラインモードを渡すことができます。

### `getTotalSize`

```tsx
getTotalSize: () => number
```

仮想化アイテムの合計サイズをピクセル単位で返します。この計測は、レンダリング時に要素を動的に計測するように選択した場合、段階的に変化します。

### `measure`

```tsx
measure: () => void
```

以前のアイテム計測をすべてリセットします。

### `measureElement`

```tsx
measureElement: (el: TItemElement | null) => void
```

構成された `measureElement` virtualizer オプションを使用して要素を計測します。コンポーネントがレンダリングされたときに（例えば React の ref コールバックプロップを使用して）virtualizer マークアップでこれを呼び出す責任があります。また `data-index` を追加する必要があります。

```tsx
 <div
  key={virtualRow.key}
  data-index={virtualRow.index}
  ref={virtualizer.measureElement}
  style={...}
>...</div>
```

デフォルトでは、`measureElement` virtualizer オプションは `getBoundingClientRect()` で要素を計測するように構成されています。

### `resizeItem`

```tsx
resizeItem: (index: number, size: number) => void
```

仮想化アイテムのサイズを手動で変更します。この関数を使用して、このインデックスに対して計算されたサイズを手動で設定します。カスタムモーフィングトランジションを使用していて、モーフィングされたアイテムのサイズを事前に知っている場合などに便利です。

また、再レンダリングを減らすために、`Virtualizer.measureElement` の代わりにスロットルされた ResizeObserver とこのメソッドを使用することもできます。

> ⚠️ `Virtualizer.measureElement` を使用してアイテムを監視しているときにアイテムのサイズを手動で変更すると、`Virtualizer.measureElement` もサイズを変更するため、予測不可能な動作が発生します。ただし、同じ virtualizer インスタンスで resizeItem または measureElement のいずれかを異なるアイテムインデックスで使用することはできます。

### `scrollRect`

```tsx
scrollRect: Rect
```

スクロール要素の現在の `Rect`。

### `shouldAdjustScrollPositionOnItemSizeChange`

```tsx
shouldAdjustScrollPositionOnItemSizeChange: undefined | ((item: VirtualItem, delta: number, instance: Virtualizer<TScrollElement, TItemElement>) => boolean)
```

shouldAdjustScrollPositionOnItemSizeChange メソッドは、動的にレンダリングされたアイテムのサイズが推定サイズと異なる場合に、スクロール位置の調整を細かく制御できます。リストの途中にジャンプして後方にスクロールすると、新しい要素のサイズが最初に推定されたサイズと異なる場合があります。この不一致により、後続のアイテムがシフトし、特にリストを後方にナビゲートするときにユーザーのスクロール体験が乱れる可能性があります。

### `isScrolling`

```tsx
isScrolling: boolean
```

リストが現在スクロール中かどうかを示すブール値フラグ。

### `
