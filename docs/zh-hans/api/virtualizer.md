---
source-updated-at: '2025-05-05T15:05:35.000Z'
translation-updated-at: '2025-05-06T22:57:33.100Z'
title: 虚拟化器 (virtualizer)
---
`Virtualizer` 类是 TanStack Virtual 的核心。通常由框架适配器为您创建 Virtualizer 实例，但您也可以直接获取虚拟化器。

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

需要虚拟化的总项目数。

### `getScrollElement`

```tsx
getScrollElement: () => TScrollElement
```

返回虚拟化器可滚动元素的函数。如果元素尚未可用，可能返回 null。

### `estimateSize`

```tsx
estimateSize: (index: number) => number
```

> 🧠 如果动态测量元素，建议估算项目可能的最大尺寸（宽度/高度，在合理范围内）。这将确保平滑滚动等功能更有可能正常工作。

此函数接收每个项目的索引，应返回每个项目的实际尺寸（如果使用 `virtualItem.measureElement` 动态测量项目，则返回估算尺寸）。根据虚拟化器的方向，此测量应返回宽度或高度。

## 可选选项

### `enabled`

```tsx
enabled?: boolean
```

设置为 `false` 可禁用 scrollElement 观察器并重置虚拟化器的状态

### `debug`

```tsx
debug?: boolean
```

设置为 `true` 可启用调试日志

### `initialRect`

```tsx
initialRect?: Rect
```

scrollElement 的初始 `Rect`。主要在 SSR 环境中运行虚拟化器时有用，否则 initialRect 将在挂载时通过 `observeElementRect` 实现计算。

### `onChange`

```tsx
onChange?: (instance: Virtualizer<TScrollElement, TItemElement>, sync: boolean) => void
```

当虚拟化器内部状态变化时触发的回调函数。接收虚拟化器实例和 sync 参数。

sync 参数表示当前是否正在进行滚动。滚动时为 `true`，滚动停止或执行其他操作（如调整大小）时为 `false`。

### `overscan`

```tsx
overscan?: number
```

在可见区域上方和下方渲染的项目数。增加此数值会增加渲染虚拟化器所需的时间，但可能减少滚动时在虚拟化器顶部和底部看到渲染缓慢的空白项目的可能性。默认值为 `1`。

### `horizontal`

```tsx
horizontal?: boolean
```

如果虚拟化器为水平方向，则设置为 `true`。

### `paddingStart`

```tsx
paddingStart?: number
```

应用于虚拟化器起始端的像素填充。

### `paddingEnd`

```tsx
paddingEnd?: number
```

应用于虚拟化器末端的像素填充。

### `scrollPaddingStart`

```tsx
scrollPaddingStart?: number
```

滚动到元素时应用于虚拟化器起始端的像素填充。

### `scrollPaddingEnd`

```tsx
scrollPaddingEnd?: number
```

滚动到元素时应用于虚拟化器末端的像素填充。

### `initialOffset`

```tsx
initialOffset?: number | (() => number)
```

应用于虚拟化器的初始偏移量。通常仅在 SSR 环境中渲染虚拟化器时有用。

### `getItemKey`

```tsx
getItemKey?: (index: number) => Key
```

此函数接收每个项目的索引，应返回该项目的唯一键。此函数的默认功能是返回项目的索引，但应尽可能覆盖此功能以返回整个集合中每个项目的唯一标识符。此函数应被记忆化以防止不必要的重新渲染。

### `rangeExtractor`

```tsx
rangeExtractor?: (range: Range) => number[]
```

此函数接收可见范围索引，应返回要渲染的索引数组。如果需要手动添加或删除虚拟化器中的项目（例如渲染粘性项目、页眉、页脚等），此功能非常有用。默认的范围提取器实现将返回可见范围索引，并导出为 `defaultRangeExtractor`。

### `scrollToFn`

```tsx
scrollToFn?: (
  offset: number,
  options: { adjustments?: number; behavior?: 'auto' | 'smooth' },
  instance: Virtualizer<TScrollElement, TItemElement>,
) => void
```

可选函数（如果提供）应实现 scrollElement 的滚动行为。调用时将传入以下参数：

- 要滚动到的 `offset`（以像素为单位）。
- 一个对象，指示估算尺寸与实际尺寸之间是否存在差异（`adjustments`）和/或是否以平滑动画调用滚动（`behaviour`）。
- 虚拟化器实例本身。

注意，内置的滚动实现导出为 `elementScroll` 和 `windowScroll`，它们由框架适配器函数（如 `useVirtualizer` 或 `useWindowVirtualizer`）自动配置。

> ⚠️ 尝试将 smoothScroll 与动态测量的元素一起使用将无效。

### `observeElementRect`

```tsx
observeElementRect: (
  instance: Virtualizer<TScrollElement, TItemElement>,
  cb: (rect: Rect) => void,
) => void | (() => void)
```

如果提供，此可选函数在 scrollElement 更改时调用，并应实现 scrollElement 的 `Rect`（包含 `width` 和 `height` 的对象）的初始测量和持续监控。调用时传入实例（您也可以通过 `instance.scrollElement` 访问 scrollElement）。内置实现导出为 `observeElementRect` 和 `observeWindowRect`，它们由框架适配器的导出函数（如 `useVirtualizer` 或 `useWindowVirtualizer`）自动配置。

### `observeElementOffset`

```tsx
observeElementOffset: (
    instance: Virtualizer<TScrollElement, TItemElement>,
    cb: (offset: number) => void,
  ) => void | (() => void)
```

如果提供，此可选函数在 scrollElement 更改时调用，并应实现 scrollElement 的滚动偏移量（数字）的初始测量和持续监控。调用时传入实例（您也可以通过 `instance.scrollElement` 访问 scrollElement）。内置实现导出为 `observeElementOffset` 和 `observeWindowOffset`，它们由框架适配器的导出函数（如 `useVirtualizer` 或 `useWindowVirtualizer`）自动配置。

### `measureElement`

```tsx
measureElement?: (
  element: TItemElement,
  entry: ResizeObserverEntry | undefined,
  instance: Virtualizer<TScrollElement, TItemElement>,
) => number
```

当虚拟化器需要动态测量项目的尺寸（宽度或高度）时调用此可选函数。

> 🧠 您可以使用 `instance.options.horizontal` 来确定应测量项目的宽度还是高度。

### `scrollMargin`

```tsx
scrollMargin?: number
```

通过此选项，可以指定滚动偏移量的起始位置。通常，此值表示滚动元素开始处与列表开始处之间的空间。这在常见场景中特别有用，例如在窗口虚拟化器前有页眉或在单个滚动元素中使用多个虚拟化器时。如果使用元素的绝对定位，应在 CSS 变换中考虑 `scrollMargin`：
```tsx
transform: `translateY(${
   virtualRow.start - rowVirtualizer.options.scrollMargin
}px)` 
``` 
要为 `scrollMargin` 动态测量值，可以使用 `getBoundingClientRect()` 或 ResizeObserver。这在虚拟列表上方的项目可能更改高度的情况下非常有用。

### `gap`

```tsx
gap?: number
```

此选项允许您设置虚拟化列表中项目之间的间距。特别适用于保持项目之间一致的视觉分隔，而无需手动调整每个项目的边距或填充。值以像素为单位指定。

### `lanes`

```tsx
lanes: number
```

列表划分的通道数（垂直列表为列，水平列表为行）。

### `isScrollingResetDelay`

```tsx
isScrollingResetDelay: number
```

此选项允许您指定在最后一个滚动事件后等待重置 isScrolling 实例属性的持续时间。默认值为 150 毫秒。

此选项的实现是为了需要一个可靠的机制来处理不同浏览器中的滚动行为。直到所有浏览器统一支持 scrollEnd 事件。

### `useScrollendEvent`

```tsx
useScrollendEvent: boolean
```

确定是否使用原生 scrollend 事件来检测滚动何时停止。如果设置为 false，则使用防抖回退在 isScrollingResetDelay 毫秒后重置 isScrolling 实例属性。默认值为 `false`。

此选项的实现是为了需要一个可靠的机制来处理不同浏览器中的滚动行为。直到所有浏览器统一支持 scrollEnd 事件。

### `isRtl`

```tsx
isRtl: boolean
```

是否反转水平滚动以支持从右到左的语言区域设置。

### `useAnimationFrameWithResizeObserver`

```tsx
useAnimationFrameWithResizeObserver: boolean
```

此选项启用将 ResizeObserver 测量包装在 requestAnimationFrame 中，以实现更平滑的更新和减少布局抖动。默认值为 `false`。

通过确保测量与渲染周期对齐，有助于防止“ResizeObserver 循环完成但未传递通知”错误。这可以提高性能并减少 UI 抖动，特别是在动态调整元素大小时。然而，由于 ResizeObserver 已经异步运行，添加 requestAnimationFrame 可能会引入轻微的测量延迟，在某些情况下可能会被注意到。如果调整大小操作轻量且不会导致重排，启用此选项可能不会带来显著好处。

## 虚拟化器实例

虚拟化器实例上提供以下属性和方法：

### `options`

```tsx
options: readonly Required<VirtualizerOptions<TScrollElement, TItemElement>>
```

虚拟化器的当前选项。此属性通过框架适配器更新，为只读。

### `scrollElement`

```tsx
scrollElement: readonly TScrollElement | null
```

虚拟化器的当前 scrollElement。此属性通过框架适配器更新，为只读。

### `getVirtualItems`

```tsx
type getVirtualItems = () => VirtualItem[]
```

返回虚拟化器当前状态的虚拟项目。

### `getVirtualIndexes`

```tsx
type getVirtualIndexes = () => number[]
```

返回虚拟化器当前状态的虚拟行索引。

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

将虚拟化器滚动到提供的像素偏移量。可以可选地传递对齐模式以将滚动锚定到 scrollElement 的特定部分。

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

将虚拟化器滚动到提供的索引项目。可以可选地传递对齐模式以将滚动锚定到 scrollElement 的特定部分。

### `getTotalSize`

```tsx
getTotalSize: () => number
```

返回虚拟化项目的总像素尺寸。如果选择在渲染时动态测量元素，此测量将逐步变化。

### `measure`

```tsx
measure: () => void
```

重置任何先前的项目测量。

### `measureElement`

```tsx
measureElement: (el: TItemElement | null) => void
```

使用配置的 `measureElement` 虚拟化器选项测量元素。您负责在虚拟化器标记中渲染组件时调用此函数（例如使用类似 React 的 ref 回调 prop）并添加 `data-index`

```tsx
 <div
  key={virtualRow.key}
  data-index={virtualRow.index}
  ref={virtualizer.measureElement}
  style={...}
>...</div>
```

默认情况下，`measureElement` 虚拟化器选项配置为使用 `getBoundingClientRect()` 测量元素。

### `resizeItem`

```tsx
resizeItem: (index: number, size: number) => void
```

手动更改虚拟化项目的尺寸。使用此函数手动设置为此索引计算的大小。在使用某些自定义变形过渡且事先知道变形项目的大小时非常有用。

您还可以将此方法与节流的 ResizeObserver 一起使用，而不是 `Virtualizer.measureElement`，以减少重新渲染。

> ⚠️ 请注意，在使用 `Virtualizer.measureElement` 监控该项目时手动更改项目的大小将导致不可预测的行为，因为 `Virtualizer.measureElement` 也在更改大小。但是，您可以在同一虚拟化器实例上使用 resizeItem 或 measureElement，但用于不同的项目索引。

### `scrollRect`

```tsx
scrollRect: Rect
```

滚动元素的当前 `Rect`。

### `shouldAdjustScrollPositionOnItemSizeChange`

```tsx
shouldAdjustScrollPositionOnItemSizeChange: undefined | ((item: VirtualItem, delta: number, instance: Virtualizer<TScrollElement, TItemElement>) => boolean)
```

shouldAdjustScrollPositionOnItemSizeChange 方法允许在动态渲染项目的尺寸与估算尺寸不同时精细控制滚动位置的调整。当跳转到列表中间并向后滚动时，新元素的尺寸可能与初始估算尺寸不同。这种差异可能导致后续项目移位，可能破坏用户的滚动体验，特别是在向后浏览列表时。

### `isScrolling`

```tsx
isScrolling: boolean
```

布尔标志，指示列表当前是否正在滚动。

### `scrollDirection`

```tsx
scrollDirection: 'forward' | 'backward' | null
```

此选项指示滚动的方向，可能值为 'forward'（向下滚动）和 'backward'（向上滚动）。没有活动滚动时值为 null。

### `scrollOffset`

```tsx
scrollOffset: number
```

此选项表示沿滚动轴的当前滚动位置。从可滚动区域的起点以像素为单位测量。
