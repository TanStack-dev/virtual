---
source-updated-at: '2024-06-01T09:52:04.000Z'
translation-updated-at: '2025-05-02T20:34:37.416Z'
title: Vue Virtual
---
# Vue Virtual

El adaptador `@tanstack/vue-virtual` es un envoltorio alrededor de la lógica virtual principal.

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Esta función retorna una instancia estándar de `Virtualizer` configurada para trabajar con un elemento HTML como scrollElement.

## `useWindowVirtualizer`

```tsx
function useWindowVirtualizer<TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<Window, TItemElement>,
    | 'getScrollElement'
    | 'observeElementRect'
    | 'observeElementOffset'
    | 'scrollToFn'
  >,
): Virtualizer<Window, TItemElement>
```

Esta función retorna una instancia de `Virtualizer` basada en la ventana, configurada para trabajar con window como scrollElement.
