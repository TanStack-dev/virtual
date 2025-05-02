---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:48:10.408Z'
title: React Virtual
---
# React Virtual

مُحَوِّل `@tanstack/react-virtual` هو غلاف حول المنطق الأساسي للتخيل (virtual logic).

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

تُعيد هذه الدالة نسخة من `Virtualizer` تعتمد على النافذة (window-based) مُهيأة للعمل مع النافذة كـ `scrollElement`.
