---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:45:05.408Z'
title: React Virtual
---
Адаптер `@tanstack/react-virtual` — это обёртка над основной логикой виртуализации.

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
