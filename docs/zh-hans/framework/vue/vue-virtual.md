---
source-updated-at: '2024-06-01T09:52:04.000Z'
translation-updated-at: '2025-04-08T03:44:10.140Z'
title: Vue Virtual
---
`@tanstack/vue-virtual` 适配器是核心虚拟逻辑的封装层。

## `useVirtualizer`

```tsx
function useVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

该函数返回一个标准的 `Virtualizer` 实例，该实例配置为使用 HTML 元素作为 滚动元素 (scrollElement)。

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

该函数返回一个基于窗口的 `Virtualizer` 实例，该实例配置为使用窗口作为 滚动元素 (scrollElement)。
