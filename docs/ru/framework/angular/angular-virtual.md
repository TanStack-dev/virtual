---
source-updated-at: '2024-08-19T19:18:26.000Z'
translation-updated-at: '2025-05-02T20:45:06.569Z'
title: Angular Virtual
---
Адаптер `@tanstack/angular-virtual` является обёрткой вокруг базовой логики виртуализации.

## `injectVirtualizer`

```ts
function injectVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    Omit<VirtualizerOptions<TScrollElement, TItemElement>, 'getScrollElement'>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  > & { scrollElement: ElementRef<TScrollElement> | TScrollElement | undefined },
): AngularVirtualizer<TScrollElement, TItemElement>
```

Эта функция возвращает экземпляр `AngularVirtualizer`, настроенный для работы с HTML-элементом в качестве `scrollElement`.

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

Эта функция возвращает экземпляр `AngularVirtualizer`, работающий с окном браузера (`window`) в качестве `scrollElement`.
