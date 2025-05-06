---
source-updated-at: '2024-06-24T18:08:48.000Z'
translation-updated-at: '2025-05-06T23:07:51.071Z'
title: Lit Virtual
---
# Lit Virtual

L'adaptateur `@tanstack/lit-virtual` est un wrapper autour de la logique virtuelle principale.

## `createVirtualizer`

```tsx
private virtualizerController = new VirtualizerController<TScrollElement, TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
)
```

Cette classe représente une instance standard de `Virtualizer` configurée pour fonctionner avec un élément HTML comme scrollElement.  
Cela créera un contrôleur Lit qui peut être accédé dans la méthode render de l'élément.

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

Cette classe représente une instance de `Virtualizer` basée sur la fenêtre, configurée pour fonctionner avec un élément HTML comme scrollElement.
