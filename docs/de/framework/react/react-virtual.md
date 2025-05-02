---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:38:49.522Z'
title: React Virtual
---
Der `@tanstack/react-virtual`-Adapter ist ein Wrapper um die zentrale Virtualisierungslogik.

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Diese Funktion gibt eine standardmäßige `Virtualizer`-Instanz zurück, die für die Verwendung mit einem HTML-Element als `scrollElement` konfiguriert ist.

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

Diese Funktion gibt eine fensterbasierte `Virtualizer`-Instanz zurück, die für die Verwendung mit dem Fenster als `scrollElement` konfiguriert ist.
