---
source-updated-at: '2024-08-19T19:18:26.000Z'
translation-updated-at: '2025-05-02T20:42:16.497Z'
title: Angular Virtual
---
L'adaptateur `@tanstack/angular-virtual` est un wrapper autour de la logique virtuelle principale.

## `injectVirtualizer`

```ts
function injectVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    Omit<VirtualizerOptions<TScrollElement, TItemElement>, 'getScrollElement'>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  > & { scrollElement: ElementRef<TScrollElement> | TScrollElement | undefined },
): AngularVirtualizer<TScrollElement, TItemElement>
```

Cette fonction retourne une instance `AngularVirtualizer` configurée pour fonctionner avec un élément HTML comme scrollElement.

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

Cette fonction retourne une instance `AngularVirtualizer` basée sur la fenêtre, configurée pour utiliser la fenêtre comme scrollElement.
