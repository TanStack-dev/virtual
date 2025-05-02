---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-05-02T20:45:05.269Z'
title: Svelte Virtual
---
# Svelte Virtual

Адаптер `@tanstack/svelte-virtual` представляет собой обёртку над основной логикой виртуализации.

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

Эта функция возвращает стандартный экземпляр `Virtualizer`, настроенный для работы с HTML-элементом в качестве `scrollElement`.

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

Эта функция возвращает экземпляр `Virtualizer`, работающий с окном браузера (`window`) в качестве `scrollElement`.
