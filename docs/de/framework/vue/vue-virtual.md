---
source-updated-at: '2024-06-01T09:52:04.000Z'
translation-updated-at: '2025-05-02T20:38:50.686Z'
title: Vue Virtual
---
# Vue Virtual

Der `@tanstack/vue-virtual`-Adapter ist ein Wrapper um die zentrale Virtualisierungslogik.

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Diese Funktion gibt eine standardmäßige `Virtualizer`-Instanz zurück, die für die Arbeit mit einem HTML-Element als `scrollElement` konfiguriert ist.

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

Diese Funktion gibt eine fensterbasierte `Virtualizer`-Instanz zurück, die für die Arbeit mit dem Fenster als `scrollElement` konfiguriert ist.
