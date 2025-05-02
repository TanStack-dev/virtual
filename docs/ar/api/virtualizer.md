---
source-updated-at: '2025-03-13T14:46:17.000Z'
translation-updated-at: '2025-05-02T20:50:32.110Z'
title: الظاهري
---
# الفِرْتوالايزر (Virtualizer)

فئة `Virtualizer` هي جوهر مكتبة TanStack Virtual. عادةً ما يتم إنشاء مثيلات الفِرْتوالايزر لك بواسطة أداة التكامل مع إطار العمل الخاص بك، ولكنك تحصل على الفِرْتوالايزر مباشرة.

```tsx
export class Virtualizer<TScrollElement = unknown, TItemElement = unknown> {
  constructor(options: VirtualizerOptions<TScrollElement, TItemElement>)
}
```

## الخيارات المطلوبة

### `count`

```tsx
count: number
```

العدد الإجمالي للعناصر المراد تخيلها (virtualize).

### `getScrollElement`

```tsx
getScrollElement: () => TScrollElement
```

دالة تُرجع العنصر القابل للتمرير للفِرْتوالايزر. قد تُرجع قيمة null إذا كان العنصر غير متاح بعد.

### `estimateSize`

```tsx
estimateSize: (index: number) => number
```

> 🧠 إذا كنت تقيس عناصرك ديناميكيًا، يُنصح بتقدير أكبر حجم ممكن (عرض/ارتفاع، ضمن حدود معقولة) لعناصرك. هذا يضمن أن ميزات مثل التمرير السلس لديها فرصة أفضل للعمل بشكل صحيح.

هذه الدالة تستقبل فهرس كل عنصر ويجب أن تُرجع الحجم الفعلي (أو الحجم المقدر إذا كنت ستقيس العناصر ديناميكيًا باستخدام `virtualItem.measureElement`) لكل عنصر. يجب أن يُرجع هذا القياس إما العرض أو الارتفاع اعتمادًا على اتجاه الفِرْتوالايزر الخاص بك.

## الخيارات الاختيارية

### `enabled`

```tsx
enabled?: boolean
```

اضبط على `false` لتعطيل مراقبي scrollElement وإعادة تعيين حالة الفِرْتوالايزر.

### `debug`

```tsx
debug?: boolean
```

اضبط على `true` لتمكين سجلات التصحيح (debug logs).

### `initialRect`

```tsx
initialRect?: Rect
```

المستطيل الابتدائي (initial `Rect`) لـ scrollElement. يكون هذا مفيدًا بشكل أساسي إذا كنت بحاجة إلى تشغيل الفِرْتوالايزر في بيئة عرض من جانب الخادم (SSR)، وإلا سيتم حساب initialRect عند التحميل بواسطة تنفيذ `observeElementRect`.

### `onChange`

```tsx
onChange?: (instance: Virtualizer<TScrollElement, TItemElement>, sync: boolean) => void
```

دالة رد اتصال (callback) تُنفّذ عندما تتغير الحالة الداخلية للفِرْتوالايزر. يتم تمرير مثيل الفِرْتوالايزر ومعلمة sync إليها.

تشير معلمة sync إلى ما إذا كان التمرير جاريًا حاليًا. تكون `true` عندما يكون التمرير مستمرًا، و`false` عندما يتوقف التمرير أو يتم تنفيذ إجراءات أخرى (مثل تغيير الحجم).

### `overscan`

```tsx
overscan?: number
```

عدد العناصر التي يجب عرضها أعلى وأسفل المنطقة المرئية. زيادة هذا الرقم ستزيد من الوقت المستغرق لعرض الفِرْتوالايزر، ولكن قد تقلل من احتمالية رؤية عناصر فارغة بطيئة العرض في أعلى وأسفل الفِرْتوالايزر عند التمرير.

### `horizontal`

```tsx
horizontal?: boolean
```

اضبط هذا على `true` إذا كان الفِرْتوالايزر الخاص بك موجهًا أفقيًا.

### `paddingStart`

```tsx
paddingStart?: number
```

الحشو المطبق على بداية الفِرْتوالايزر بالبكسل.

### `paddingEnd`

```tsx
paddingEnd?: number
```

الحشو المطبق على نهاية الفِرْتوالايزر بالبكسل.

### `scrollPaddingStart`

```tsx
scrollPaddingStart?: number
```

الحشو المطبق على بداية الفِرْتوالايزر بالبكسل عند التمرير إلى عنصر.

### `scrollPaddingEnd`

```tsx
scrollPaddingEnd?: number
```

الحشو المطبق على نهاية الفِرْتوالايزر بالبكسل عند التمرير إلى عنصر.

### `initialOffset`

```tsx
initialOffset?: number | (() => number)
```

الإزاحة الابتدائية المطبقة على الفِرْتوالايزر. يكون هذا مفيدًا عادةً فقط إذا كنت تعرض الفِرْتوالايزر في بيئة عرض من جانب الخادم (SSR).

### `getItemKey`

```tsx
getItemKey?: (index: number) => Key
```

هذه الدالة تستقبل فهرس كل عنصر ويجب أن تُرجع مفتاحًا فريدًا لذلك العنصر. الوظيفة الافتراضية لهذه الدالة هي إرجاع فهرس العنصر، ولكن يجب عليك تجاوز هذا عندما يكون ممكنًا لإرجاع معرف فريد لكل عنصر عبر المجموعة بأكملها. يجب حفظ هذه الدالة (memoize) لمنع إعادة التصيير غير الضرورية.

### `rangeExtractor`

```tsx
rangeExtractor?: (range: Range) => number[]
```

هذه الدالة تستقبل فهارس النطاق المرئي ويجب أن تُرجع مصفوفة من الفهارس للعرض. يكون هذا مفيدًا إذا كنت بحاجة إلى إضافة أو إزالة عناصر من الفِرْتوالايزر يدويًا بغض النظر عن النطاق المرئي، مثل عرض العناصر اللاصقة (sticky items)، والعناوين، والتذييلات، إلخ. تنفيذ extractor النطاق الافتراضي سيرجع فهارس النطاق المرئي ويتم تصديره كـ `defaultRangeExtractor`.

### `scrollToFn`

```tsx
scrollToFn?: (
  offset: number,
  options: { adjustments?: number; behavior?: 'auto' | 'smooth' },
  instance: Virtualizer<TScrollElement, TItemElement>,
) => void
```

دالة اختيارية (إذا تم توفيرها) يجب أن تنفذ سلوك التمرير لـ scrollElement الخاص بك. سيتم استدعاؤها بالوسائط التالية:

- `offset` (بالبكسل) للتمرير نحوه.
- كائن يشير إلى ما إذا كان هناك فرق بين الحجم المقدر والحجم الفعلي (`adjustments`) و/أو ما إذا تم استدعاء التمرير بتحريك سلس (`behaviour`).
- مثيل الفِرْتوالايزر نفسه.

لاحظ أن تنفيذات التمرير المضمنة يتم تصديرها كـ `elementScroll` و`windowScroll`، والتي يتم تكوينها تلقائيًا بواسطة دوال تكامل إطار العمل مثل `useVirtualizer` أو `useWindowVirtualizer`.

> ⚠️ محاولة استخدام smoothScroll مع العناصر المقاسة ديناميكيًا لن تعمل.

### `observeElementRect`

```tsx
observeElementRect: (
  instance: Virtualizer<TScrollElement, TItemElement>,
  cb: (rect: Rect) => void,
) => void | (() => void)
```

دالة اختيارية إذا تم توفيرها يتم استدعاؤها عندما يتغير scrollElement ويجب أن تنفذ القياس الأولي والمراقبة المستمرة لـ `Rect` لـ scrollElement (كائن به `width` و`height`). يتم استدعاؤها بالمثيل (والذي يمنحك أيضًا الوصول إلى scrollElement عبر `instance.scrollElement`. يتم تصدير التنفيذات المضمنة كـ `observeElementRect` و`observeWindowRect` والتي يتم تكوينها تلقائيًا لك بواسطة دوال تكامل إطار العمل المصدرة مثل `useVirtualizer` أو `useWindowVirtualizer`.

### `observeElementOffset`

```tsx
observeElementOffset: (
    instance: Virtualizer<TScrollElement, TItemElement>,
    cb: (offset: number) => void,
  ) => void | (() => void)
```

دالة اختيارية إذا تم توفيرها يتم استدعاؤها عندما يتغير scrollElement ويجب أن تنفذ القياس الأولي والمراقبة المستمرة لإزاحة التمرير لـ scrollElement (رقم). يتم استدعاؤها بالمثيل (والذي يمنحك أيضًا الوصول إلى scrollElement عبر `instance.scrollElement`. يتم تصدير التنفيذات المضمنة كـ `observeElementOffset` و`observeWindowOffset` والتي يتم تكوينها تلقائيًا لك بواسطة دوال تكامل إطار العمل المصدرة مثل `useVirtualizer` أو `useWindowVirtualizer`.

### `measureElement`

```tsx
measureElement?: (
  element: TItemElement,
  entry: ResizeObserverEntry | undefined,
  instance: Virtualizer<TScrollElement, TItemElement>,
) => number
```

هذه الدالة الاختيارية تُستدعى عندما يحتاج الفِرْتوالايزر إلى قياس حجم (عرض أو ارتفاع) عنصر ما ديناميكيًا.

> 🧠 يمكنك استخدام `instance.options.horizontal` لتحديد ما إذا كان يجب قياس عرض أو ارتفاع العنصر.

### `scrollMargin`

```tsx
scrollMargin?: number
```

بهذا الخيار، يمكنك تحديد مكان بدء إزاحة التمرير. عادةً، تمثل هذه القيمة المسافة بين بداية عنصر التمرير وبداية القائمة. يكون هذا مفيدًا بشكل خاص في السيناريوهات الشائعة مثل عندما يكون لديك رأس يسبق window virtualizer أو عندما يتم استخدام عدة virtualizers داخل عنصر تمرير واحد. إذا كنت تستخدم تحديد المواقع المطلق (absolute positioning) للعناصر، يجب أن تأخذ في الاعتبار `scrollMargin` في تحويل CSS الخاص بك:
```tsx
transform: `translateY(${
   virtualRow.start - rowVirtualizer.options.scrollMargin
}px)` 
``` 
لقياس قيمة `scrollMargin` ديناميكيًا، يمكنك استخدام `getBoundingClientRect()` أو ResizeObserver. يكون هذا مفيدًا في السيناريوهات عندما قد يتغير ارتفاع العناصر فوق قائمتك الافتراضية.

### `gap`

```tsx
gap?: number
```

يسمح لك هذا الخيار بتعيين التباعد بين العناصر في القائمة الافتراضية. يكون مفيدًا بشكل خاص للحفاظ على فصل مرئي متسق بين العناصر دون الحاجة إلى ضبط هامش أو حشو كل عنصر يدويًا. يتم تحديد القيمة بالبكسل.

### `lanes`

```tsx
lanes: number
```

عدد الممرات (lanes) التي تنقسم إليها القائمة (المعروفة أيضًا بالأعمدة للقوائم الرأسية والصفوف للقوائم الأفقية).

### `isScrollingResetDelay`

```tsx
isScrollingResetDelay: number
```

يسمح لك هذا الخيار بتحديد المدة الزمنية للانتظار بعد آخر حدث تمرير قبل إعادة تعيين خاصية المثيل isScrolling. القيمة الافتراضية هي 150 مللي ثانية.

يتم تنفيذ هذا الخيار بسبب الحاجة إلى آلية موثوقة للتعامل مع سلوك التمرير عبر المتصفحات المختلفة. حتى تدعم جميع المتصفحات حدث scrollEnd بشكل موحد.

### `useScrollendEvent`

```tsx
useScrollendEvent: boolean
```

يحدد ما إذا كان سيتم استخدام حدث scrollend الأصلي للكشف عن توقف التمرير. إذا تم تعيينه على false، يتم استخدام fallback debounced لإعادة تعيين خاصية المثيل isScrolling بعد isScrollingResetDelay مللي ثانية. القيمة الافتراضية هي `false`.

يتم تنفيذ هذا الخيار بسبب الحاجة إلى آلية موثوقة للتعامل مع سلوك التمرير عبر المتصفحات المختلفة. حتى تدعم جميع المتصفحات حدث scrollEnd بشكل موحد.

### `isRtl`

```tsx
isRtl: boolean
```

ما إذا كان سيتم عكس التمرير الأفقي لدعم اللغات من اليمين إلى اليسار.

### `useAnimationFrameWithResizeObserver`

```tsx
useAnimationFrameWithResizeObserver: boolean
```

يمكّن هذا الخيار من تغليف قياسات ResizeObserver في requestAnimationFrame للتحديثات الأكثر سلاسة وتقليل التمزق في التخطيط (layout thrashing). القيمة الافتراضية هي `false`.

يساعد في منع خطأ "ResizeObserver loop completed with undelivered notifications" عن طريق التأكد من أن القياسات تتماشى مع دورة التصيير. يمكن أن يحسن هذا الأداء ويقلل من ارتعاش واجهة المستخدم، خاصة عند تغيير حجم العناصر ديناميكيًا. ومع ذلك، نظرًا لأن ResizeObserver يعمل بالفعل بشكل غير متزامن، فقد يؤدي إضافة requestAnimationFrame إلى تأخير طفيف في القياسات، والذي قد يكون ملحوظًا في بعض الحالات. إذا كانت عمليات تغيير الحجم خفيفة ولا تسبب إعادة تدفقات (reflows)، فقد لا يوفر تمكين هذا الخيار فوائد كبيرة.

## مثيل الفِرْتوالايزر

الخصائص والطرق التالية متاحة على مثيل الفِرْتوالايزر:

### `options`

```tsx
options: readonly Required<VirtualizerOptions<TScrollElement, TItemElement>>
```

الخيارات الحالية للفِرْتوالايزر. يتم تحديث هذه الخاصية عبر أداة تكامل إطار العمل الخاص بك وهي للقراءة فقط.

### `scrollElement`

```tsx
scrollElement: readonly TScrollElement | null
```

عنصر التمرير الحالي للفِرْتوالايزر. يتم تحديث هذه الخاصية عبر أداة تكامل إطار العمل الخاص بك وهي للقراءة فقط.

### `getVirtualItems`

```tsx
type getVirtualItems = () => VirtualItem[]
```

تُرجع العناصر الافتراضية للحالة الحالية للفِرْتوالايزر.

### `getVirtualIndexes`

```tsx
type getVirtualIndexes = () => number[]
```

تُرجع فهارس الصفوف الافتراضية للحالة الحالية للفِرْتوالايزر.

### `scrollToOffset`

```tsx
scrollToOffset: (
  toOffset: number,
  options?: {
    align?: 'start' | 'center' | 'end' | 'auto',
    behavior?: 'auto' | 'smooth'
  }
) => void
```

يُمرر الفِرْتوالايزر إلى إزاحة البكسل المقدمة. يمكنك اختياريًا تمرير وضع محاذاة لربط التمرير بجزء معين من scrollElement.

### `scrollToIndex`

```tsx
scrollToIndex: (
  index: number,
  options?: {
    align?: 'start' | 'center' | 'end' | 'auto',
    behavior?: 'auto' | 'smooth'
  }
) => void
```

يُمرر الفِرْتوالايزر إلى عنصر الفهرس المقدم. يمكنك اختياريًا تمرير وضع محاذاة لربط التمرير بجزء معين من scrollElement.

### `getTotalSize`

```tsx
getTotalSize: () => number
```

تُرجع الحجم الإجمالي بالبكسل للعناصر الافتراضية. سيتغير هذا القياس تدريجيًا إذا اخترت قياس عناصرك ديناميكيًا أثناء عرضها.

### `measure`

```tsx
measure: () => void
```

يعيد تعيين أي قياسات سابقة للعناصر.

### `measureElement`

```tsx
measureElement: (el: TItemElement | null) => void
```

يقيس العنصر باستخدام خيار `measureElement` المكون للفِرْتوالايزر الخاص بك. أنت مسؤول عن استدعاء هذا في ترميز الفِرْتوالايزر الخاص بك عندما يتم عرض المكون (على سبيل المثال، باستخدام شيء مثل خاصية رد الاتصال ref في React) بالإضافة إلى إضافة `data-index`

```tsx
 <div
  key={virtualRow.key}
  data-index={virtualRow.index}
  ref={virtualizer.measureElement}
  style={...}
>...</div>
```

بشكل افتراضي، يتم تكوين خيار `measureElement` للفِرْتوالايزر لقياس العناصر باستخدام `getBoundingClientRect()`.

### `resizeItem`

```tsx
resizeItem: (index: number, size: number) => void
```

قم بتغيير حجم العنصر الافتراضي يدويًا. استخدم هذه الدالة لتعيين الحجم المحسوب لهذا الفهرس يدويًا. يكون مفيدًا في الحالات عند استخدام بعض انتقالات التحويل (morphing transitions) المخصصة وأنت تعرف حجم العنصر المحول مسبقًا.

يمكنك أيضًا استخدام هذه الطريقة مع ResizeObserver محدود (throttled) بدلاً من `Virtualizer.measureElement` لتقليل إعادة التصيير.

> ⚠️ يرجى العلم أن تغيير حجم العنصر يدويًا عند استخدام `Virtualizer.measureElement` لمراقبة ذلك العنصر، سيؤدي إلى سلوك غير متوقع لأن `Virtualizer.measureElement` يغير الحجم أيضًا. ومع ذلك، يمكنك استخدام إما resizeItem أو measureElement في نفس مثيل الفِرْتوالايزر ولكن على فهارس عناصر مختلفة.

### `scrollRect`

```tsx
scrollRect: Rect
```

المستطيل الحالي (`Rect`) لعنصر التمرير.

### `shouldAdjustScrollPositionOnItemSizeChange`

```tsx
shouldAdjustScrollPosition
