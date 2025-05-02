---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:38:50.823Z'
title: Svelte Virtual
---
Der `@tanstack/svelte-virtual`-Adapter ist ein Wrapper um die zentrale Virtualisierungslogik.

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Diese Funktion gibt eine standardmäßige `Virtualizer`-Instanz zurück, die für die Verwendung mit einem HTML-Element als `scrollElement` konfiguriert ist.

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

Diese Funktion gibt eine fensterbasierte `Virtualizer`-Instanz zurück, die für die Verwendung mit dem Fenster als `scrollElement` konfiguriert ist.
