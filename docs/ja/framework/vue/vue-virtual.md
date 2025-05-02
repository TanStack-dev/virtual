---
source-updated-at: '2024-06-01T09:52:04.000Z'
translation-updated-at: '2025-05-02T20:30:09.521Z'
title: Vue Virtual
---
`@tanstack/vue-virtual`アダプターは、コアの仮想化ロジックをラップしたものです。

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

この関数は、スクロール要素としてHTML要素と連携するように設定された標準の`Virtualizer`インスタンスを返します。

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

この関数は、スクロール要素としてウィンドウと連携するように設定されたウィンドウベースの`Virtualizer`インスタンスを返します。
