---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T15:24:32.469Z'
title: Svelte Virtual
---
`@tanstack/svelte-virtual` 配接器是核心虛擬邏輯的封裝層。

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

此函數會回傳一個標準的 `Virtualizer` 實例，該實例配置為以 HTML 元素作為 scrollElement 來運作。

## `createWindowVirtualizer`

```tsx
function createWindowVirtualizer<TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<Window, TItemElement>,
    | 'getScrollElement'
    | 'observeElementRect'
    | 'observeElementOffset'
    | 'scrollToFn'
  >,
): Virtualizer<Window, TItemElement>
```

此函數會回傳一個基於視窗的 `Virtualizer` 實例，該實例配置為以視窗作為 scrollElement 來運作。
