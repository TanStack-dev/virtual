---
source-updated-at: '2024-08-19T19:18:26.000Z'
translation-updated-at: '2025-05-02T20:38:50.397Z'
title: Angular Virtual
---
Der `@tanstack/angular-virtual`-Adapter ist ein Wrapper um die zentrale Virtualisierungslogik.

## `injectVirtualizer`

```ts
function injectVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    Omit<VirtualizerOptions<TScrollElement, TItemElement>, 'getScrollElement'>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  > & { scrollElement: ElementRef<TScrollElement> | TScrollElement | undefined },
): AngularVirtualizer<TScrollElement, TItemElement>
```

Diese Funktion gibt eine `AngularVirtualizer`-Instanz zurück, die für die Arbeit mit einem HTML-Element als `scrollElement` konfiguriert ist.

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

Diese Funktion gibt eine fensterbasierte `AngularVirtualizer`-Instanz zurück, die für die Arbeit mit dem Fenster als `scrollElement` konfiguriert ist.
