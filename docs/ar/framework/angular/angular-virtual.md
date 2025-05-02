---
source-updated-at: '2024-08-19T19:18:26.000Z'
translation-updated-at: '2025-05-02T20:48:11.378Z'
title: Angular Virtual
---
محول `@tanstack/angular-virtual` هو غلاف حول المنطق الأساسي للتمرير الافتراضي.

## `injectVirtualizer`

```ts
function injectVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    Omit<VirtualizerOptions<TScrollElement, TItemElement>, 'getScrollElement'>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  > & { scrollElement: ElementRef<TScrollElement> | TScrollElement | undefined },
): AngularVirtualizer<TScrollElement, TItemElement>
```

تُرجع هذه الدالة نسخة من `AngularVirtualizer` مُهيأة للعمل مع عنصر HTML كـ scrollElement.

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

تُرجع هذه الدالة نسخة من `AngularVirtualizer` تعتمد على النافذة ومُهيأة للعمل مع النافذة كـ scrollElement.
