---
source-updated-at: '2024-06-01T09:52:04.000Z'
translation-updated-at: '2025-05-02T20:45:05.097Z'
title: Vue Virtual
---
Адаптер `@tanstack/vue-virtual` — это обёртка над основной логикой виртуализации.

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Эта функция возвращает стандартный экземпляр `Virtualizer`, настроенный для работы с HTML-элементом в качестве `scrollElement`.

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

Эта функция возвращает экземпляр `Virtualizer`, работающий с окном браузера в качестве `scrollElement`.
