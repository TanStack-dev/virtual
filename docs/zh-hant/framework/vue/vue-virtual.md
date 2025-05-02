---
source-updated-at: '2024-06-01T09:52:04.000Z'
translation-updated-at: '2025-05-02T15:23:49.906Z'
title: Vue Virtual
---
`@tanstack/vue-virtual` 配接器是對核心虛擬邏輯的封裝。

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

此函數返回一個標準的 `Virtualizer` 實例，該實例配置為以 HTML 元素作為 scrollElement 運作。

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

此函數返回一個基於視窗的 `Virtualizer` 實例，該實例配置為以視窗作為 scrollElement 運作。
