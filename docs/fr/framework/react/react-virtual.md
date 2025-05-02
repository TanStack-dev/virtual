---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:42:15.674Z'
title: React Virtual
---
# React Virtual

L'adaptateur `@tanstack/react-virtual` est un wrapper autour de la logique virtuelle principale.

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
