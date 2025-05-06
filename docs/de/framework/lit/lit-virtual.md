---
source-updated-at: '2024-06-24T18:08:48.000Z'
translation-updated-at: '2025-05-06T23:05:13.366Z'
title: Lit Virtual
---
Der `@tanstack/lit-virtual`-Adapter ist ein Wrapper um die zentrale Virtualisierungslogik.

## `createVirtualizer`

```tsx
private virtualizerController = new VirtualizerController<TScrollElement, TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
)
```

Diese Klasse repräsentiert eine standardmäßige `Virtualizer`-Instanz, die für die Arbeit mit einem HTML-Element als `scrollElement` konfiguriert ist.  
Dies erstellt einen Lit-Controller, auf den in der `render`-Methode des Elements zugegriffen werden kann.

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

Diese Klasse repräsentiert eine fensterbasierte `Virtualizer`-Instanz, die für die Arbeit mit einem HTML-Element als `scrollElement` konfiguriert ist.
