---
source-updated-at: '2024-08-29T09:26:23.000Z'
translation-updated-at: '2025-04-08T03:44:10.055Z'
title: 虚拟项 (virtual item)
---
`VirtualItem` 对象表示由虚拟化器 (virtualizer) 返回的单个虚拟项 (virtual item)。它包含在虚拟化器的滚动元素 (scroll element) 坐标空间中渲染该项所需的信息以及其他有用的属性/方法。

```tsx
export interface VirtualItem {
  key: string | number | bigint
  index: number
  start: number
  end: number
  size: number
}
```

每个 `VirtualItem` 对象上可用的属性和方法如下：

### `key`

```tsx
key: string | number | bigint
```

该项的唯一键 (key)。默认情况下为该项的索引 (index)，但应通过虚拟化器 (virtualizer) 的 `getItemKey` 选项进行配置。

### `index`

```tsx
index: number
```

该项的索引 (index)。

### `start`

```tsx
start: number
```

该项的起始像素偏移量 (offset)。通常映射到 CSS 属性或变换 (transform)，如 `top/left` 或 `translateX/translateY`。

### `end`

```tsx
end: number
```

该项的结束像素偏移量 (offset)。大多数布局不需要此值，但为了提供便利，我们仍然保留了它。

### `size`

```tsx
size: number
```

该项的大小 (size)。通常映射到 CSS 属性如 `width/height`。在使用 `VirtualItem.measureElement` 方法测量该项之前，此值为虚拟化器 (virtualizer) 的 `estimateSize` 选项返回的估计大小。测量后（如果选择测量），此值将变为 `measureElement` 虚拟化器选项返回的数字（默认配置为使用 `getBoundingClientRect()` 测量元素）。

### `lane`

```tsx
lane: number
```

该项的通道 (lane) 索引 (index)。在常规列表中始终为 `0`，但在瀑布流布局 (masonry) 中会变得有用（详见变量示例）。
