---
source-updated-at: '2025-03-13T14:46:17.000Z'
translation-updated-at: '2025-04-08T03:44:10.090Z'
title: 虚拟化器 (virtualizer)
---
`Virtualizer` 类是 TanStack Virtual 的核心。虚拟化器 (virtualizer) 实例通常由框架适配器为你创建，但你会直接获取到该虚拟化器 (virtualizer)。

```tsx
export class Virtualizer<TScrollElement = unknown, TItemElement = unknown> {
  constructor(options: VirtualizerOptions<TScrollElement, TItemElement>)
}
```

## 必填选项

### `count`

```tsx
count: number
```

需要虚拟化的总项数。

### `getScrollElement`

```tsx
getScrollElement: () => TScrollElement
```

返回虚拟化器 (virtualizer) 的可滚动元素 (scroll element) 的函数。如果元素尚未可用，可能返回 null。

### `estimateSize`

```tsx
estimateSize: (index: number) => number
```

> 🧠 如果你需要动态测量元素大小，建议预估一个合理的最大可能尺寸（宽度/高度）。这将确保平滑滚动等功能更有可能正常工作。

此函数接收每个项的索引 (index)，并应返回每个项的实际大小（或如果你打算使用 `virtualItem.measureElement` 动态测量项，则返回预估大小）。根据虚拟化器 (virtualizer) 的方向，此测量应返回宽度或高度。

## 可选选项

### `enabled`

```tsx
enabled?: boolean
```

设置为 `false` 可禁用滚动元素 (scroll element) 观察器并重置虚拟化器 (virtualizer) 的状态

### `debug`

```tsx
debug?: boolean
```

设置为 `true` 可启用调试日志

### `initialRect`

```tsx
initialRect?: Rect
```

滚动元素 (scroll element) 的初始 `Rect`。这主要在需要在 SSR 环境中运行虚拟化器 (virtualizer) 时有用，否则初始矩形 (rect) 将由 `observeElementRect` 实现在挂载时计算。

### `onChange`

```tsx
onChange?: (instance: Virtualizer<TScrollElement, TItemElement>, sync: boolean) => void
```

当虚拟化器 (virtualizer) 内部状态变化时触发的回调函数。它接收虚拟化器 (virtualizer) 实例和同步参数。

同步参数表示滚动是否正在进行。滚动进行时为 `true`，滚动停止或执行其他操作（如调整大小）时为 `false`。

### `overscan`

```tsx
overscan?: number
```

在可见区域上方和下方渲染的项数。增加此数值会增加虚拟化器 (virtualizer) 的渲染时间，但可能减少滚动时在虚拟化器 (virtualizer) 顶部和底部看到渲染缓慢空白项的可能性。

### `horizontal`

```tsx
horizontal?: boolean
```

如果你的虚拟化器 (virtualizer) 是水平方向的，请设置为 `true`。

### `paddingStart`

```tsx
paddingStart?: number
```

应用于虚拟化器 (virtualizer) 起始位置的填充（像素）。

### `paddingEnd`

```tsx
paddingEnd?: number
```

应用于虚拟化器 (virtualizer) 结束位置的填充（像素）。

### `scrollPaddingStart`

```tsx
scrollPaddingStart?: number
```

滚动到元素时应用于虚拟化器 (virtualizer) 起始位置的填充（像素）。

### `scrollPaddingEnd`

```tsx
scrollPaddingEnd?: number
```

滚动到元素时应用于虚拟化器 (virtualizer) 结束位置的填充（像素）。

### `initialOffset`

```tsx
initialOffset?: number | (() => number)
```

应用于虚拟化器 (virtualizer) 的初始偏移量 (offset)。这通常仅在 SSR 环境中渲染虚拟化器 (virtualizer) 时有用。

### `getItemKey`

```tsx
getItemKey?: (index: number) => Key
```

此函数接收每个项的索引 (index)，并应返回该项的唯一键 (key)。此函数的默认功能是返回项的索引 (index)，但应尽可能覆盖此功能以返回整个集合中每个项的唯一标识符。此函数应被记忆化以防止不必要的重新渲染。

### `rangeExtractor`

```tsx
rangeExtractor?: (range: Range) => number[]
```

此函数接收可见范围索引 (index)，并应返回要渲染的索引 (index) 数组。如果你需要手动添加或移除虚拟化器 (virtualizer) 中的项（例如渲染粘性项、页眉、页脚等），这很有用。默认的范围提取器实现将返回可见范围索引 (index)，并导出为 `defaultRangeExtractor`。

### `scrollToFn`

```tsx
scrollToFn?: (
  offset: number,
  options: { adjustments?: number; behavior?: 'auto' | 'smooth' },
  instance: Virtualizer<TScrollElement, TItemElement>,
) => void
```

一个可选函数（如果提供）应实现滚动元素 (scroll element) 的滚动行为。它将使用以下参数调用：

- 要滚动到的 `offset`（像素）。
- 一个对象，指示预估大小与实际大小之间是否存在差异（`adjustments`）和/或是否以平滑动画调用滚动（`behaviour`）。
- 虚拟化器 (virtualizer) 实例本身。

请注意，内置的滚动实现导出为 `elementScroll` 和 `windowScroll`，它们由框架适配器函数（如 `useVirtualizer` 或 `useWindowVirtualizer`）自动配置。

> ⚠️ 尝试将 smoothScroll 与动态测量元素一起使用将不起作用。

### `observeElementRect`

```tsx
observeElementRect: (
  instance: Virtualizer<TScrollElement, TItemElement>,
  cb: (rect: Rect) => void,
) => void | (() => void)
```

一个可选函数，如果提供，则在滚动元素 (scroll element) 更改时调用，并应实现滚动元素 (scroll element) 的 `Rect`（包含 `width` 和 `height` 的对象）的初始测量和持续监控。它通过实例调用（你也可以通过 `instance.scrollElement` 访问滚动元素 (scroll element)）。内置实现导出为 `observeElementRect` 和 `observeWindowRect`，它们由框架适配器的导出函数（如 `useVirtualizer` 或 `useWindowVirtualizer`）自动配置。

### `observeElementOffset`

```tsx
observeElementOffset: (
    instance: Virtualizer<TScrollElement, TItemElement>,
    cb: (offset: number) => void,
  ) => void | (() => void)
```

一个可选函数，如果提供，则在滚动元素 (scroll element) 更改时调用，并应实现滚动元素 (scroll element) 的滚动偏移量 (offset)（数字）的初始测量和持续监控。它通过实例调用（你也可以通过 `instance.scrollElement` 访问滚动元素 (scroll element)）。内置实现导出为 `observeElementOffset` 和 `observeWindowOffset`，它们由框架适配器的导出函数（如 `useVirtualizer` 或 `useWindowVirtualizer`）自动配置。

### `measureElement`

```tsx
measureElement?: (
  element: TItemElement,
  entry: ResizeObserverEntry | undefined,
  instance: Virtualizer<TScrollElement, TItemElement>,
) => number
```

此可选函数在虚拟化器 (virtualizer) 需要动态测量项的大小（宽度或高度）时调用。

> 🧠 你可以使用 `instance.options.horizontal` 来确定应测量项的宽度还是高度。

### `scrollMargin`

```tsx
scrollMargin?: number
```

通过此选项，你可以指定滚动偏移量 (offset) 的起始位置。通常，此值表示滚动元素 (scroll element) 开始处与列表开始处之间的空间。这在常见场景中特别有用，例如当你在窗口虚拟化器 (virtualizer) 前有页眉，或在单个滚动元素 (scroll element) 中使用多个虚拟化器 (virtualizer) 时。如果你使用元素的绝对定位，应在 CSS 变换 (transform) 中考虑 `scrollMargin`：
```tsx
transform: `translateY(${
   virtualRow.start - rowVirtualizer.options.scrollMargin
}px)` 
``` 
要动态测量 `scrollMargin` 的值，可以使用 `getBoundingClientRect()` 或 ResizeObserver。这在虚拟列表上方的项可能改变高度的情况下很有帮助。

### `gap`

```tsx
gap?: number
```

此选项允许你设置虚拟化列表中项之间的间距。它特别适用于保持项之间一致的视觉分隔，而无需手动调整每个项的边距或填充。值以像素为单位指定。

### `lanes`

```tsx
lanes: number
```

列表划分的通道 (lane) 数（垂直列表为列，水平列表为行）。

### `isScrollingResetDelay`

```tsx
isScrollingResetDelay: number
```

此选项允许你指定在最后一个滚动事件后等待重置 isScrolling 实例属性的持续时间。默认值为 150 毫秒。

此选项的实现源于需要一种可靠的机制来处理不同浏览器间的滚动行为。直到所有浏览器统一支持 scrollEnd 事件。

### `useScrollendEvent`

```tsx
useScrollendEvent: boolean
```

确定是否使用原生 scrollend 事件来检测滚动何时停止。如果设置为 false，则使用防抖回退在 isScrollingResetDelay 毫秒后重置 isScrolling 实例属性。默认值为 `false`。

此选项的实现源于需要一种可靠的机制来处理不同浏览器间的滚动行为。直到所有浏览器统一支持 scrollEnd 事件。

### `isRtl`

```tsx
isRtl: boolean
```

是否反转水平滚动以支持从右到左的语言环境。

### `useAnimationFrameWithResizeObserver`

```tsx
useAnimationFrameWithResizeObserver: boolean
```

此选项启用将 ResizeObserver 测量包装在 requestAnimationFrame 中，以实现更平滑的更新和减少布局抖动。默认值为 `false`。

它通过确保测量与渲染周期对齐，有助于防止“ResizeObserver 循环已完成但未传递通知”错误。这可以提高性能并减少 UI 抖动，特别是在动态调整元素大小时。然而，由于 ResizeObserver 已经异步运行，添加 requestAnimationFrame 可能会引入轻微的测量延迟，在某些情况下可能明显。如果调整大小操作轻量且不会导致重排，启用此选项可能不会带来显著好处。

## 虚拟化器 (virtualizer) 实例

虚拟化器 (virtualizer) 实例上提供以下属性和方法：

### `options`

```tsx
options: readonly Required<VirtualizerOptions<TScrollElement, TItemElement>>
```

虚拟化器 (virtualizer) 的当前选项。此属性通过框架适配器更新，为只读。

### `scrollElement`

```tsx
scrollElement: readonly TScrollElement | null
```

虚拟化器 (virtualizer) 的当前滚动元素 (scroll element)。此属性通过框架适配器更新，为只读。

### `getVirtualItems`

```tsx
type getVirtualItems = () => VirtualItem[]
```

返回虚拟化器 (virtualizer) 当前状态的虚拟项 (virtual item)。

### `getVirtualIndexes`

```tsx
type getVirtualIndexes = () => number[]
```

返回虚拟化器 (virtualizer) 当前状态的虚拟行索引 (index)。

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

将虚拟化器 (virtualizer) 滚动到提供的像素偏移量 (offset)。你可以选择传递对齐模式以将滚动锚定到滚动元素 (scroll element) 的特定部分。

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

将虚拟化器 (virtualizer) 滚动到提供的索引 (index) 的项。你可以选择传递对齐模式以将滚动锚定到滚动元素 (scroll element) 的特定部分。

### `getTotalSize`

```tsx
getTotalSize: () => number
```

返回虚拟化项的总大小（像素）。如果你选择在渲染时动态测量元素，此测量将逐步变化。

### `measure`

```tsx
measure: () => void
```

重置任何先前的项测量。

### `measureElement`

```tsx
measureElement: (el: TItemElement | null) => void
```

使用你配置的 `measureElement` 虚拟化器 (virtualizer) 选项测量元素。你负责在虚拟化器 (virtualizer) 标记中渲染组件时调用此函数（例如使用类似 React 的 ref 回调属性），并添加 `data-index`

```tsx
 <div
  key={virtualRow.key}
  data-index={virtualRow.index}
  ref={virtualizer.measureElement}
  style={...}
>...</div>
```

默认情况下，`measureElement` 虚拟化器 (virtualizer) 选项配置为使用 `getBoundingClientRect()` 测量元素。

### `resizeItem`

```tsx
resizeItem: (index: number, size: number) => void
```

手动更改虚拟化项的大小。使用此函数手动设置为此索引 (index) 计算的大小。在使用某些自定义变形过渡并且你事先知道变形项的大小时很有用。

你也可以将此方法与节流的 ResizeObserver 一起使用，而不是 `Virtualizer.measureElement`，以减少重新渲染。

> ⚠️ 请注意，当使用 `Virtualizer.measureElement` 监控该项时手动更改项的大小会导致不可预测的行为，因为 `Virtualizer.measureElement` 也在更改大小。但是，你可以在同一虚拟化器 (virtualizer) 实例的不同项索引 (index) 上使用 resizeItem 或 measureElement 之一。

### `scrollRect`

```tsx
scrollRect: Rect
```

滚动元素 (scroll element) 的当前 `Rect`。

### `shouldAdjustScrollPositionOnItemSizeChange`

```tsx
shouldAdjustScrollPositionOnItemSizeChange: undefined | ((item: VirtualItem, delta: number, instance: Virtualizer<TScrollElement, TItemElement>) => boolean)
```

shouldAdjustScrollPositionOnItemSizeChange 方法可以精细控制动态渲染项的大小与预估大小不同时滚动位置的调整。当跳转到列表中间并向后滚动时，新元素的大小可能与初始预估大小不同。这种差异可能导致后续项移位，可能破坏用户的滚动体验，特别是在向后浏览列表时。

### `isScrolling`

```tsx
isScrolling: boolean
```

布尔标志，指示列表当前是否正在滚动。

### `scrollDirection`

```tsx
scrollDirection: 'forward' | 'backward' | null
```

此选项指示滚动的方向，可能值为 'forward'（向下滚动）和 'backward'（向上滚动）。当没有活动滚动时，值为 null。

### `scrollOffset`

```tsx
scrollOffset: number
```

此选项表示沿滚动轴的当前滚动位置。它从可滚动区域的起点以像素为单位测量。
