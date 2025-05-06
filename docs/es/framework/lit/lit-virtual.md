---
source-updated-at: '2024-06-24T18:08:48.000Z'
translation-updated-at: '2025-05-06T23:02:41.438Z'
title: Lit Virtual
---
El adaptador `@tanstack/lit-virtual` es un envoltorio alrededor de la lógica virtual principal.

## `createVirtualizer`

```tsx

private virtualizerController = new VirtualizerController<TScrollElement, TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
)
```

Esta clase representa una instancia estándar de `Virtualizer` configurada para funcionar con un elemento HTML como scrollElement.  
Esto creará un Lit Controller (Controlador de Lit) que puede ser accedido en el método render del elemento.

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

Esta clase representa una instancia de `Virtualizer` basada en ventana, configurada para funcionar con un elemento HTML como scrollElement.
