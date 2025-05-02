---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:35:05.271Z'
title: Svelte Virtual
---
# Svelte Virtual

El adaptador `@tanstack/svelte-virtual` es un envoltorio alrededor de la lógica virtual principal.

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Esta función devuelve una instancia estándar de `Virtualizer` configurada para trabajar con un elemento HTML como scrollElement.

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

Esta función devuelve una instancia de `Virtualizer` basada en la ventana, configurada para trabajar con window como scrollElement.
