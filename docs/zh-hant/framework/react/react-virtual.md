---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T15:25:01.231Z'
title: React Virtual
---
`@tanstack/react-virtual` 轉接器是核心虛擬邏輯的封裝層。

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

此函數會返回一個標準的 `Virtualizer` 實例，該實例配置為以 HTML 元素作為 scrollElement 運作。

## `useWindowVirtualizer`

```tsx
function useWindowVirtualizer<TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<Window, TItemElement>,
    | 'getScrollElement'
    | 'observeElementRect'
    | 'observeElementOffset'
    | 'scrollToFn'
  >,
): Virtualizer<Window, TItemElement>
```

此函數會返回一個基於視窗的 `Virtualizer` 實例，該實例配置為以視窗作為 scrollElement 運作。
