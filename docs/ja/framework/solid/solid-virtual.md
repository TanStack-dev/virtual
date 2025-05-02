---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:29:22.370Z'
title: Solid Virtual
---
`@tanstack/solid-virtual`アダプターは、コアの仮想化ロジックをラップしたものです。

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

この関数は、HTML要素を`scrollElement`として動作するように設定された標準の`Virtualizer`インスタンスを返します。

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

この関数は、ウィンドウを`scrollElement`として動作するように設定されたウィンドウベースの`Virtualizer`インスタンスを返します。
