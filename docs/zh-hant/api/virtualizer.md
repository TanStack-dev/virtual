---
source-updated-at: '2025-03-13T14:46:17.000Z'
translation-updated-at: '2025-05-02T15:27:27.557Z'
title: 虛擬化器 (Virtualizer)
---
`Virtualizer` 類別是 TanStack Virtual 的核心。通常框架適配器會自動為你建立 Virtualizer 實例，但你也可以直接取得 virtualizer 實體。

```tsx
export class Virtualizer<TScrollElement = unknown, TItemElement = unknown> {
  constructor(options: VirtualizerOptions<TScrollElement, TItemElement>)
}
```

## 必要選項

### `count`

```tsx
count: number
```

需要虛擬化的項目總數。

### `getScrollElement`

```tsx
getScrollElement: () => TScrollElement
```

一個函式，回傳 virtualizer 的可滾動元素。如果元素尚未可用，可以回傳 null。

### `estimateSize`

```tsx
estimateSize: (index: number) => number
```

> 🧠 如果你要動態測量元素大小，建議估計項目可能的最大尺寸（在合理範圍內的寬度/高度）。這將確保平滑滾動等功能有更高的機率正常運作。

此函式會接收每個項目的索引，並應回傳該項目的實際大小（或如果你打算使用 `virtualItem.measureElement` 動態測量項目，則回傳估計大小）。此測量應根據 virtualizer 的方向回傳寬度或高度。

## 可選選項

### `enabled`

```tsx
enabled?: boolean
```

設為 `false` 可停用 scrollElement 觀察器並重設 virtualizer 的狀態

### `debug`

```tsx
debug?: boolean
```

設為 `true` 可啟用除錯日誌

### `initialRect`

```tsx
initialRect?: Rect
```

scrollElement 的初始 `Rect`。這主要在需要於 SSR 環境中運行 virtualizer 時有用，否則 initialRect 會在掛載時由 `observeElementRect` 實作計算。

### `onChange`

```tsx
onChange?: (instance: Virtualizer<TScrollElement, TItemElement>, sync: boolean) => void
```

當 virtualizer 內部狀態變化時觸發的回呼函式。它會接收 virtualizer 實例和 sync 參數。

sync 參數表示當前是否正在滾動。當滾動進行中時為 `true`，當滾動停止或正在執行其他操作（例如調整大小）時為 `false`。

### `overscan`

```tsx
overscan?: number
```

在可見區域上方和下方渲染的項目數量。增加此數字會增加渲染 virtualizer 所需的時間，但可能減少在滾動時看到頂部和底部慢速渲染空白項目的可能性。

### `horizontal`

```tsx
horizontal?: boolean
```

如果你的 virtualizer 是水平方向的，請將此設為 `true`。

### `paddingStart`

```tsx
paddingStart?: number
```

以像素為單位，應用於 virtualizer 起始端的內距。

### `paddingEnd`

```tsx
paddingEnd?: number
```

以像素為單位，應用於 virtualizer 結束端的內距。

### `scrollPaddingStart`

```tsx
scrollPaddingStart?: number
```

滾動到元素時，以像素為單位應用於 virtualizer 起始端的內距。

### `scrollPaddingEnd`

```tsx
scrollPaddingEnd?: number
```

滾動到元素時，以像素為單位應用於 virtualizer 結束端的內距。

### `initialOffset`

```tsx
initialOffset?: number | (() => number)
```

應用於 virtualizer 的初始偏移量。這通常只在 SSR 環境中渲染 virtualizer 時有用。

### `getItemKey`

```tsx
getItemKey?: (index: number) => Key
```

此函式會接收每個項目的索引，並應回傳該項目的唯一鍵。此函式的預設功能是回傳項目的索引，但你應盡可能覆寫此功能以回傳整個集合中每個項目的唯一識別碼。此函式應被記憶化以防止不必要的重新渲染。

### `rangeExtractor`

```tsx
rangeExtractor?: (range: Range) => number[]
```

此函式接收可見範圍的索引，並應回傳要渲染的索引陣列。如果你需要手動新增或移除 virtualizer 中的項目（例如渲染固定項目、標頭、頁尾等），這會很有用。預設的範圍提取器實作會回傳可見範圍的索引，並以 `defaultRangeExtractor` 匯出。

### `scrollToFn`

```tsx
scrollToFn?: (
  offset: number,
  options: { adjustments?: number; behavior?: 'auto' | 'smooth' },
  instance: Virtualizer<TScrollElement, TItemElement>,
) => void
```

一個可選函式（如果提供）應實作 scrollElement 的滾動行為。它會以以下參數呼叫：

- 要滾動到的 `offset`（以像素為單位）。
- 一個物件，表示估計大小與實際大小之間是否存在差異（`adjustments`）和/或滾動是否以平滑動畫呼叫（`behaviour`）。
- virtualizer 實例本身。

請注意，內建的滾動實作會以 `elementScroll` 和 `windowScroll` 匯出，它們會由框架適配器函式（如 `useVirtualizer` 或 `useWindowVirtualizer`）自動配置。

> ⚠️ 嘗試將 smoothScroll 與動態測量的元素一起使用是無效的。

### `observeElementRect`

```tsx
observeElementRect: (
  instance: Virtualizer<TScrollElement, TItemElement>,
  cb: (rect: Rect) => void,
) => void | (() => void)
```

一個可選函式，如果提供，會在 scrollElement 變更時呼叫，並應實作 scrollElement 的 `Rect`（具有 `width` 和 `height` 的物件）的初始測量和持續監控。它會以實例（你也可以透過 `instance.scrollElement` 存取 scrollElement）呼叫。內建實作會以 `observeElementRect` 和 `observeWindowRect` 匯出，它們會由框架適配器的匯出函式（如 `useVirtualizer` 或 `useWindowVirtualizer`）自動為你配置。

### `observeElementOffset`

```tsx
observeElementOffset: (
    instance: Virtualizer<TScrollElement, TItemElement>,
    cb: (offset: number) => void,
  ) => void | (() => void)
```

一個可選函式，如果提供，會在 scrollElement 變更時呼叫，並應實作 scrollElement 的滾動偏移量（一個數字）的初始測量和持續監控。它會以實例（你也可以透過 `instance.scrollElement` 存取 scrollElement）呼叫。內建實作會以 `observeElementOffset` 和 `observeWindowOffset` 匯出，它們會由框架適配器的匯出函式（如 `useVirtualizer` 或 `useWindowVirtualizer`）自動為你配置。

### `measureElement`

```tsx
measureElement?: (
  element: TItemElement,
  entry: ResizeObserverEntry | undefined,
  instance: Virtualizer<TScrollElement, TItemElement>,
) => number
```

此可選函式會在 virtualizer 需要動態測量項目的大小（寬度或高度）時呼叫。

> 🧠 你可以使用 `instance.options.horizontal` 來判斷應測量項目的寬度還是高度。

### `scrollMargin`

```tsx
scrollMargin?: number
```

透過此選項，你可以指定滾動偏移量的起始位置。通常，此值代表滾動元素開頭與清單開頭之間的空間。這在常見情境中特別有用，例如當你在視窗 virtualizer 前有標頭，或在單一滾動元素中使用多個 virtualizer 時。如果你使用元素的絕對定位，你應在 CSS transform 中考慮 `scrollMargin`：
```tsx
transform: `translateY(${
   virtualRow.start - rowVirtualizer.options.scrollMargin
}px)` 
``` 
要動態測量 `scrollMargin` 的值，你可以使用 `getBoundingClientRect()` 或 ResizeObserver。這在虛擬清單上方的項目可能變更高度的情境中很有幫助。

### `gap`

```tsx
gap?: number
```

此選項允許你設定虛擬化清單中項目之間的間距。這對於在不手動調整每個項目的 margin 或 padding 的情況下保持一致的視覺分隔特別有用。該值以像素為單位指定。

### `lanes`

```tsx
lanes: number
```

清單劃分的通道數（垂直清單的欄數或水平清單的列數）。

### `isScrollingResetDelay`

```tsx
isScrollingResetDelay: number
```

此選項允許你指定在最後一個滾動事件後等待多久才重設 isScrolling 實例屬性。預設值為 150 毫秒。

此選項的實作是出於需要一個可靠的機制來處理不同瀏覽器間的滾動行為。直到所有瀏覽器都統一支援 scrollEnd 事件。

### `useScrollendEvent`

```tsx
useScrollendEvent: boolean
```

決定是否使用原生的 scrollend 事件來偵測滾動何時停止。如果設為 false，則會使用防抖回退在 isScrollingResetDelay 毫秒後重設 isScrolling 實例屬性。預設值為 `false`。

此選項的實作是出於需要一個可靠的機制來處理不同瀏覽器間的滾動行為。直到所有瀏覽器都統一支援 scrollEnd 事件。

### `isRtl`

```tsx
isRtl: boolean
```

是否反轉水平滾動以支援從右到左的語言區域設定。

### `useAnimationFrameWithResizeObserver`

```tsx
useAnimationFrameWithResizeObserver: boolean
```

此選項啟用將 ResizeObserver 測量包裝在 requestAnimationFrame 中，以實現更平滑的更新和減少佈局抖動。預設值為 `false`。

它透過確保測量與渲染週期對齊，有助於防止「ResizeObserver 循環完成但未傳遞通知」的錯誤。這可以提高效能並減少 UI 抖動，特別是在動態調整元素大小時。然而，由於 ResizeObserver 已經是非同步運行的，加入 requestAnimationFrame 可能會引入測量的輕微延遲，在某些情況下可能會被注意到。如果調整大小操作是輕量級的且不會導致重排，啟用此選項可能不會帶來顯著的好處。

## Virtualizer 實例

以下屬性和方法可在 virtualizer 實例上使用：

### `options`

```tsx
options: readonly Required<VirtualizerOptions<TScrollElement, TItemElement>>
```

virtualizer 的當前選項。此屬性會透過你的框架適配器更新，並且是唯讀的。

### `scrollElement`

```tsx
scrollElement: readonly TScrollElement | null
```

virtualizer 的當前 scrollElement。此屬性會透過你的框架適配器更新，並且是唯讀的。

### `getVirtualItems`

```tsx
type getVirtualItems = () => VirtualItem[]
```

回傳 virtualizer 當前狀態的虛擬項目。

### `getVirtualIndexes`

```tsx
type getVirtualIndexes = () => number[]
```

回傳 virtualizer 當前狀態的虛擬列索引。

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

將 virtualizer 滾動到提供的像素偏移量。你可以選擇性地傳遞對齊模式，以將滾動錨定到 scrollElement 的特定部分。

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

將 virtualizer 滾動到提供的索引項目。你可以選擇性地傳遞對齊模式，以將滾動錨定到 scrollElement 的特定部分。

### `getTotalSize`

```tsx
getTotalSize: () => number
```

回傳虛擬化項目的總大小（以像素為單位）。如果你選擇在渲染時動態測量元素，此測量會逐步變更。

### `measure`

```tsx
measure: () => void
```

重設任何先前的項目測量。

### `measureElement`

```tsx
measureElement: (el: TItemElement | null) => void
```

使用你配置的 `measureElement` virtualizer 選項來測量元素。你需要在 virtualizer 標記中渲染元件時負責呼叫此函式（例如使用類似 React 的 ref 回呼 prop），同時新增 `data-index`

```tsx
 <div
  key={virtualRow.key}
  data-index={virtualRow.index}
  ref={virtualizer.measureElement}
  style={...}
>...</div>
```

預設情況下，`measureElement` virtualizer 選項配置為使用 `getBoundingClientRect()` 測量元素。

### `resizeItem`

```tsx
resizeItem: (index: number, size: number) => void
```

手動變更虛擬化項目的大小。使用此函式手動設定為此索引計算的大小。在使用某些自訂變形過渡且你事先知道變形項目的大小時很有用。

你也可以將此方法與節流的 ResizeObserver 一起使用，而不是 `Virtualizer.measureElement`，以減少重新渲染。

> ⚠️ 請注意，當使用 `Virtualizer.measureElement` 監控該項目時，手動變更項目的大小會導致不可預測的行為，因為 `Virtualizer.measureElement` 也在變更大小。然而，你可以在同一個 virtualizer 實例中的不同項目索引上使用 resizeItem 或 measureElement 其中之一。

### `scrollRect`

```tsx
scrollRect: Rect
```

scroll 元素的當前 `Rect`。

### `shouldAdjustScrollPositionOnItemSizeChange`

```tsx
shouldAdjustScrollPositionOnItemSizeChange: undefined | ((item: VirtualItem, delta: number, instance: Virtualizer<TScrollElement, TItemElement>) => boolean)
```

shouldAdjustScrollPositionOnItemSizeChange 方法可精細控制當動態渲染的項目大小與估計大小不同時，滾動位置的調整。當跳到清單中間並向後滾動時，新元素的大小可能與初始估計大小不同。這種差異可能導致後續項目移位，可能在使用者向後滾動清單時破壞滾動體驗。

### `isScrolling`

```tsx
isScrolling: boolean
```

表示清單當前是否正在滾動的布林旗標。

### `scrollDirection`

```tsx
scrollDirection: 'forward' | 'backward' | null
```

此選項表示滾動的方向，可能的值為向下滾動的 'forward' 和向上滾動的 'backward'。當沒有活動滾動時，該值為 null。

### `scrollOffset`

```tsx
scrollOffset: number
```

此選項表示沿滾動軸的當前滾動位置。它以像素為單位測量，從可滾動區域的起點開始計算。
