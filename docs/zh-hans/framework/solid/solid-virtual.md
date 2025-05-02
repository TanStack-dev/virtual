---
source-updated-at: '2024-01-25T21:23:10.000Z'
translation-updated-at: '2025-04-08T03:44:10.263Z'
title: Solid Virtual
---
`@tanstack/solid-virtual` 适配器是核心虚拟化逻辑的封装层。

## `createVirtualizer`

```tsx
function createVirtualizer<TScrollElement, TItemElement = unknown>(
  options: PartialKeys<
    VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
  >,
): Virtualizer<TScrollElement, TItemElement>
```

该函数返回一个标准的 `Virtualizer` 实例，配置为使用 HTML 元素作为 滚动元素 (scroll element)。

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

该函数返回一个基于窗口的 `Virtualizer` 实例，配置为使用 window 对象作为 滚动元素 (scroll element)。
