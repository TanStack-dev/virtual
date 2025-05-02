---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:48:10.870Z'
title: Solid Virtual
---
```solid-virtual@tanstack/` هو عبارة عن غلاف (wrapper) حول المنطق الأساسي للتخيل الافتراضي.

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

تُرجع هذه الدالة نسخة قياسية من `Virtualizer` مهيأة للعمل مع عنصر HTML كـ `scrollElement`.

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

تُرجع هذه الدالة نسخة من `Virtualizer` تعتمد على النافذة (window) ومهيأة للعمل مع النافذة كـ `scrollElement`.
