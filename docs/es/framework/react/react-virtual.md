---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:34:24.079Z'
title: React Virtual
---
El adaptador `@tanstack/react-virtual` es un envoltorio alrededor de la lógica central de virtualización.

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Esta función retorna una instancia estándar de `Virtualizer` configurada para trabajar con un elemento HTML como el scrollElement.

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

Esta función retorna una instancia de `Virtualizer` basada en la ventana, configurada para trabajar con el objeto window como el scrollElement.
