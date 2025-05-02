---
source-updated-at: '2024-06-01T09:52:04.000Z'
translation-updated-at: '2025-05-02T20:48:10.741Z'
title: Vue Virtual
---
# Vue Virtual

مُحَوِّل `@tanstack/vue-virtual` هو غلاف حول المنطق الأساسي للعناصر الافتراضية.

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

تُعيد هذه الدالة نسخة قياسية من `Virtualizer` مُهيأة للعمل مع عنصر HTML كـ `scrollElement`.

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

تُعيد هذه الدالة نسخة من `Virtualizer` تعتمد على النافذة ومُهيأة للعمل مع النافذة كـ `scrollElement`.
