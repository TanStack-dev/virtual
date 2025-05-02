---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:45:05.501Z'
title: Solid Virtual
---
# Solid Virtual

Адаптер `@tanstack/solid-virtual` является обёрткой вокруг основной логики виртуализации.

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Эта функция возвращает стандартный экземпляр `Virtualizer`, настроенный для работы с HTML-элементом в качестве scrollElement.

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

Эта функция возвращает экземпляр `Virtualizer`, работающий с окном браузера (window) в качестве scrollElement.
