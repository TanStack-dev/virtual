---
source-updated-at: '2024-06-24T18:08:48.000Z'
translation-updated-at: '2025-05-06T23:00:01.826Z'
title: Lit Virtual
---
`@tanstack/lit-virtual`アダプターは、コアの仮想ロジックをラップしたものです。

## `createVirtualizer`

```tsx
private virtualizerController = new VirtualizerController<TScrollElement, TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
)
```

このクラスは、スクロール要素としてHTML要素と連携するように設定された標準的な`Virtualizer`インスタンスを表します。
これはLitコントローラーを作成し、要素のレンダーメソッド内でアクセス可能です。

```tsx
render() {
    const virtualizer = this.virtualizerController.getVirtualizer();
    const virtualItems = virtualizer.getVirtualItems();
} 
)
```

## `createWindowVirtualizer`

```tsx
private windowVirtualizerController = new WindowVirtualizerController<TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TItemElement>,
    'getScrollElement' | 'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
```

このクラスは、スクロール要素としてHTML要素と連携するように設定されたウィンドウベースの`Virtualizer`インスタンスを表します。
