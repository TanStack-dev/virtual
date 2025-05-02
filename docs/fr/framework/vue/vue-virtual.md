---
source-updated-at: '2024-06-01T09:52:04.000Z'
translation-updated-at: '2025-05-02T20:42:15.863Z'
title: Vue Virtual
---
# Vue Virtual

L'adaptateur `@tanstack/vue-virtual` est un wrapper autour de la logique virtuelle principale.

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Cette fonction retourne une instance standard de `Virtualizer` configurée pour fonctionner avec un élément HTML comme scrollElement.

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

Cette fonction retourne une instance de `Virtualizer` basée sur la fenêtre, configurée pour utiliser la fenêtre comme scrollElement.
