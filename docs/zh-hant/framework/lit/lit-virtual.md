---
source-updated-at: '2024-06-24T18:08:48.000Z'
translation-updated-at: '2025-05-06T22:57:47.358Z'
title: Lit Virtual
---
`@tanstack/lit-virtual` 配接器是核心虛擬邏輯的封裝層。

## `createVirtualizer`

```tsx
private virtualizerController = new VirtualizerController<TScrollElement, TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
)
```

此類別代表一個標準的 `Virtualizer` 實例，配置為與 HTML 元素作為 scrollElement 協同工作。這將建立一個可在元素渲染方法中存取的 Lit 控制器 (Lit Controller)。

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

此類別代表一個基於視窗 (window-based) 的 `Virtualizer` 實例，配置為與 HTML 元素作為 scrollElement 協同工作。
