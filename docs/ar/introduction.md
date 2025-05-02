---
source-updated-at: '2024-11-25T13:01:52.000Z'
translation-updated-at: '2025-05-02T20:48:25.464Z'
title: المقدمة
---
# مقدمة  

TanStack Virtual هو أداة واجهة مستخدم "بدون رأس" (headless UI) لتخيل (virtualizing) قوائم طويلة من العناصر في JS/TS، React، Vue، Svelte، Solid، Lit، و Angular. إنها ليست مكونًا (component) وبالتالي لا توفر أو تعرض أي ترميز (markup) أو أنماط (styles) نيابة عنك. بينما يتطلب ذلك منك بعض الترميز والأنماط، ستحتفظ بتحكم بنسبة 100٪ في أنماطك وتصميمك وتنفيذك.

## المُخَيِّل (Virtualizer)  

في صميم TanStack Virtual يوجد المُخَيِّل (Virtualizer). يمكن توجيه المُخَيِّل على المحور الرأسي (الإفتراضي) أو المحور الأفقي، مما يجعل من الممكن تحقيق التخيل (virtualization) الرأسي والأفقي وحتى الشبيه بالشبكة (grid-like) من خلال الجمع بين تكوينات المحورين معًا.  

إليك مثالًا سريعًا لكيفية تخيل قائمة طويلة داخل عنصر div باستخدام TanStack Virtual في React:  

```tsx
import { useVirtualizer } from '@tanstack/react-virtual';

function App() {
  // العنصر القابل للتمرير للقائمة
  const parentRef = React.useRef(null)

  // المُخَيِّل
  const rowVirtualizer = useVirtualizer({
    count: 10000,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 35,
  })

  return (
    <>
      {/* العنصر القابل للتمرير للقائمة */}
      <div
        ref={parentRef}
        style={{
          height: `400px`,
          overflow: 'auto', // اجعله قابلًا للتمرير!
        }}
      >
        {/* العنصر الداخلي الكبير لحفظ جميع العناصر */}
        <div
          style={{
            height: `${rowVirtualizer.getTotalSize()}px`,
            width: '100%',
            position: 'relative',
          }}
        >
          {/* فقط العناصر المرئية في المُخَيِّل، موضوعة يدويًا لتكون في العرض */}
          {rowVirtualizer.getVirtualItems().map((virtualItem) => (
            <div
              key={virtualItem.key}
              style={{
                position: 'absolute',
                top: 0,
                left: 0,
                width: '100%',
                height: `${virtualItem.size}px`,
                transform: `translateY(${virtualItem.start}px)`,
              }}
            >
              Row {virtualItem.index}
            </div>
          ))}
        </div>
      </div>
    </>
  )
}
```  

لنستكشف المزيد من الأمثلة!
