---
source-updated-at: '2024-06-24T18:08:48.000Z'
translation-updated-at: '2025-05-06T23:13:15.681Z'
title: Lit Virtual
---
```markdown
`@tanstack/lit-virtual` هو مُحَوِّل (adapter) يغلف المنطق الأساسي للعناصر الافتراضية (virtual logic).

## `createVirtualizer`

```tsx
private virtualizerController = new VirtualizerController<TScrollElement, TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TScrollElement, TItemElement>,
    'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
)
```

تمثل هذه الفئة نسخة قياسية من `Virtualizer` مُهيأة للعمل مع عنصر HTML كعنصر التمرير (scrollElement).  
سيؤدي هذا إلى إنشاء وحدة تحكم (Controller) من Lit يمكن الوصول إليها في طريقة عرض العنصر (render method).

```tsx
render() {
    const virtualizer = this.virtualizerController.getVirtualizer();
    const virtualItems = virtualizer.getVirtualItems();
} 
)
```

## `createWindowVirtualizer`

```tsx
private windowVirtualizerController = new WindowVirtualizerController<TItemElement = unknown>(
    options: PartialKeys< VirtualizerOptions<TItemElement>,
    'getScrollElement' | 'observeElementRect' | 'observeElementOffset' | 'scrollToFn'
```

تمثل هذه الفئة نسخة من `Virtualizer` تعتمد على النافذة (window-based) ومُهيأة للعمل مع عنصر HTML كعنصر التمرير (scrollElement).
```
