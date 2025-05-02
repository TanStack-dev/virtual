---
source-updated-at: '2024-08-29T09:26:23.000Z'
translation-updated-at: '2025-05-02T15:23:10.370Z'
title: 虛擬項目 (VirtualItem)
---
`VirtualItem` 物件代表虛擬化器 (virtualizer) 返回的單一項目，其中包含在虛擬化器的 scrollElement 座標空間內渲染該項目所需的資訊，以及其他實用的屬性/方法。

```tsx
export interface VirtualItem {
  key: string | number | bigint
  index: number
  start: number
  end: number
  size: number
}
```

每個 VirtualItem 物件都提供以下屬性和方法：

### `key`

```tsx
key: string | number | bigint
```

項目的唯一鍵值 (key)。預設為項目索引，但應透過 Virtualizer 選項中的 `getItemKey` 進行設定。

### `index`

```tsx
index: number
```

項目的索引值。

### `start`

```tsx
start: number
```

項目的起始像素偏移量。通常會對應到 CSS 屬性或變形效果，例如 `top/left` 或 `translateX/translateY`。

### `end`

```tsx
end: number
```

項目的結束像素偏移量。大多數佈局不需要此值，但我們仍提供此屬性以備不時之需。

### `size`

```tsx
size: number
```

項目的尺寸。通常會對應到 CSS 屬性如 `width/height`。在使用 `VirtualItem.measureElement` 方法測量項目之前，此值會是虛擬化器選項 `estimateSize` 返回的預估尺寸。測量項目後（如有進行測量），此值會變成虛擬化器選項 `measureElement` 返回的數值（預設設定為使用 `getBoundingClientRect()` 測量元素）。

### `lane`

```tsx
lane: number
```

項目的通道索引 (lane index)。在一般清單中此值始終為 `0`，但在瀑布流佈局 (masonry layouts) 中會變得有用（詳見變數範例）。
