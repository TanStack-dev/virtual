---
source-updated-at: '2024-06-24T18:08:48.000Z'
translation-updated-at: '2025-05-06T22:55:43.560Z'
title: Lit Virtual
---
`@tanstack/lit-virtual` 适配器是对核心虚拟逻辑的封装。

## `createVirtualizer`

```tsx
private virtualizerController = new VirtualizerController<TScrollElement, TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
)
```

该类代表一个标准的 `Virtualizer` 实例，配置为使用 HTML 元素作为 scrollElement。  
这将创建一个可在元素渲染方法中访问的 Lit 控制器 (Lit Controller)。

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

该类代表基于窗口的 `Virtualizer` 实例，配置为使用 HTML 元素作为 scrollElement。
