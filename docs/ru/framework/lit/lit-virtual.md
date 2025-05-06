---
source-updated-at: '2024-06-24T18:08:48.000Z'
translation-updated-at: '2025-05-06T23:10:35.943Z'
title: Lit Virtual
---
Адаптер `@tanstack/lit-virtual` является обёрткой над основной логикой виртуализации.

## `createVirtualizer`

```tsx
private virtualizerController = new VirtualizerController<TScrollElement, TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
)
```

Этот класс представляет стандартный экземпляр `Virtualizer`, настроенный для работы с HTML-элементом в качестве scrollElement.  
Он создаёт Lit Controller, доступный в методе render элемента.

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

Этот класс представляет window-based (основанный на окне) экземпляр `Virtualizer`, настроенный для работы с HTML-элементом в качестве scrollElement.
