---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:48:10.945Z'
title: Svelte Virtual
---
# Svelte Virtual

المُكيف `@tanstack/svelte-virtual` هو غلاف حول المنطق الأساسي للعناصر الافتراضية.

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

تُرجع هذه الدالة نسخة قياسية من `Virtualizer` مُهيأة للعمل مع عنصر HTML كعنصر التمرير (scrollElement).

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

تُرجع هذه الدالة نسخة من `Virtualizer` تعتمد على النافذة (window-based) ومُهيأة للعمل مع النافذة كعنصر التمرير (scrollElement).
