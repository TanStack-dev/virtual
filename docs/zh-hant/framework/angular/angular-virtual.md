---
source-updated-at: '2024-08-19T19:18:26.000Z'
translation-updated-at: '2025-05-02T15:24:47.795Z'
title: Angular Virtual
---
`@tanstack/angular-virtual` 配接器是核心虛擬邏輯的封裝層。

## `injectVirtualizer`

```ts
function injectVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    Omit<VirtualizerOptions<TScrollElement, TItemElement>, 'getScrollElement'>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  > & { scrollElement: ElementRef<TScrollElement> | TScrollElement | undefined },
): AngularVirtualizer<TScrollElement, TItemElement>
```

此函數會回傳一個 `AngularVirtualizer` 實例，該實例配置為以 HTML 元素作為 scrollElement 運作。

## `injectWindowVirtualizer`

```ts
function injectWindowVirtualizer<TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<Window, TItemElement>,
    | 'getScrollElement'
    | 'observeElementRect'
    | 'observeElementOffset'
    | 'scrollToFn'
  >,
): AngularVirtualizer<Window, TItemElement>
```

此函數會回傳一個基於視窗的 `AngularVirtualizer` 實例，該實例配置為以視窗作為 scrollElement 運作。
