---
source-updated-at: '2024-08-19T19:18:26.000Z'
translation-updated-at: '2025-05-02T20:34:52.175Z'
title: Angular Virtual
---
El adaptador `@tanstack/angular-virtual` es un envoltorio alrededor de la lógica virtual principal.

## `injectVirtualizer`

```ts
function injectVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    Omit<VirtualizerOptions<TScrollElement, TItemElement>, 'getScrollElement'>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  > & { scrollElement: ElementRef<TScrollElement> | TScrollElement | undefined },
): AngularVirtualizer<TScrollElement, TItemElement>
```

Esta función devuelve una instancia de `AngularVirtualizer` configurada para trabajar con un elemento HTML como scrollElement.

## `injectWindowVirtualizer`

```ts
function injectWindowVirtualizer<TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<Window, TItemElement>,
    | 'getScrollElement'
    | 'observeElementRect'
    | 'observeElementOffset'
    | 'scrollToFn'
  >,
): AngularVirtualizer<Window, TItemElement>
```

Esta función devuelve una instancia de `AngularVirtualizer` basada en la ventana, configurada para trabajar con la ventana como scrollElement.
