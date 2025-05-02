---
source-updated-at: '2024-08-19T19:18:26.000Z'
translation-updated-at: '2025-04-08T03:44:10.219Z'
title: Angular Virtual
---
`@tanstack/angular-virtual` 适配器是对核心虚拟化逻辑的封装。

## `injectVirtualizer`

```ts
function injectVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    Omit<VirtualizerOptions<TScrollElement, TItemElement>, 'getScrollElement'>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  > & { scrollElement: ElementRef<TScrollElement> | TScrollElement | undefined },
): AngularVirtualizer<TScrollElement, TItemElement>
```

该函数返回一个配置为使用 HTML 元素作为 滚动元素 (scroll element) 的 `AngularVirtualizer` 实例。

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

该函数返回一个基于窗口的 `AngularVirtualizer` 实例，配置为使用窗口作为 滚动元素 (scroll element)。
