---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:30:35.940Z'
title: Svelte Virtual
---
`@tanstack/svelte-virtual`アダプターは、コアのバーチャルロジックをラップしたものです。

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

この関数は、スクロール要素としてHTML要素と連携するように設定された標準的な`Virtualizer`インスタンスを返します。

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

この関数は、スクロール要素としてウィンドウと連携するように設定されたウィンドウベースの`Virtualizer`インスタンスを返します。
