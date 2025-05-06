---
source-updated-at: '2025-05-05T15:05:35.000Z'
translation-updated-at: '2025-05-06T23:07:36.854Z'
title: Virtualizer
---
Die `Virtualizer`-Klasse ist der Kern von TanStack Virtual. Virtualizer-Instanzen werden normalerweise für Sie durch Ihren Framework-Adapter erstellt, aber Sie erhalten den Virtualizer direkt.

```tsx
export class Virtualizer<TScrollElement = unknown, TItemElement = unknown> {
  constructor(options: VirtualizerOptions<TScrollElement, TItemElement>)
}
```

## Erforderliche Optionen

### `count`

```tsx
count: number
```

Die Gesamtanzahl der zu virtualisierenden Elemente.

### `getScrollElement`

```tsx
getScrollElement: () => TScrollElement
```

Eine Funktion, die das scrollbare Element für den Virtualizer zurückgibt. Sie kann null zurückgeben, wenn das Element noch nicht verfügbar ist.

### `estimateSize`

```tsx
estimateSize: (index: number) => number
```

> 🧠 Wenn Sie Ihre Elemente dynamisch messen, wird empfohlen, die größtmögliche Größe (Breite/Höhe, im Rahmen des Zumutbaren) Ihrer Elemente zu schätzen. Dies stellt sicher, dass Funktionen wie sanftes Scrollen besser funktionieren.

Diese Funktion erhält den Index jedes Elements und sollte die tatsächliche Größe (oder geschätzte Größe, wenn Sie Elemente dynamisch mit `virtualItem.measureElement` messen) für jedes Element zurückgeben. Diese Messung sollte je nach Ausrichtung Ihres Virtualizers entweder die Breite oder Höhe zurückgeben.

## Optionale Optionen

### `enabled`

```tsx
enabled?: boolean
```

Auf `false` setzen, um ScrollElement-Observer zu deaktivieren und den Zustand des Virtualizers zurückzusetzen.

### `debug`

```tsx
debug?: boolean
```

Auf `true` setzen, um Debug-Logs zu aktivieren.

### `initialRect`

```tsx
initialRect?: Rect
```

Das initiale `Rect` des ScrollElements. Dies ist hauptsächlich nützlich, wenn Sie den Virtualizer in einer SSR-Umgebung ausführen müssen, ansonsten wird das initialRect beim Mount durch die `observeElementRect`-Implementierung berechnet.

### `onChange`

```tsx
onChange?: (instance: Virtualizer<TScrollElement, TItemElement>, sync: boolean) => void
```

Eine Callback-Funktion, die ausgelöst wird, wenn sich der interne Zustand des Virtualizers ändert. Sie erhält die Virtualizer-Instanz und den sync-Parameter.

Der sync-Parameter gibt an, ob gerade gescrollt wird. Er ist `true`, wenn das Scrollen läuft, und `false`, wenn das Scrollen gestoppt wurde oder andere Aktionen (wie z.B. Größenänderungen) durchgeführt werden.

### `overscan`

```tsx
overscan?: number
```

Die Anzahl der Elemente, die oberhalb und unterhalb des sichtbaren Bereichs gerendert werden sollen. Eine Erhöhung dieser Zahl verlängert die Renderzeit des Virtualizers, verringert aber die Wahrscheinlichkeit, langsam renderende leere Elemente oben und unten im Virtualizer beim Scrollen zu sehen. Der Standardwert ist `1`.

### `horizontal`

```tsx
horizontal?: boolean
```

Auf `true` setzen, wenn Ihr Virtualizer horizontal ausgerichtet ist.

### `paddingStart`

```tsx
paddingStart?: number
```

Der Abstand, der am Anfang des Virtualizers in Pixeln angewendet werden soll.

### `paddingEnd`

```tsx
paddingEnd?: number
```

Der Abstand, der am Ende des Virtualizers in Pixeln angewendet werden soll.

### `scrollPaddingStart`

```tsx
scrollPaddingStart?: number
```

Der Abstand, der am Anfang des Virtualizers in Pixeln angewendet werden soll, wenn zu einem Element gescrollt wird.

### `scrollPaddingEnd`

```tsx
scrollPaddingEnd?: number
```

Der Abstand, der am Ende des Virtualizers in Pixeln angewendet werden soll, wenn zu einem Element gescrollt wird.

### `initialOffset`

```tsx
initialOffset?: number | (() => number)
```

Der initiale Offset, der auf den Virtualizer angewendet werden soll. Dies ist normalerweise nur nützlich, wenn Sie den Virtualizer in einer SSR-Umgebung rendern.

### `getItemKey`

```tsx
getItemKey?: (index: number) => Key
```

Diese Funktion erhält den Index jedes Elements und sollte einen eindeutigen Schlüssel für dieses Element zurückgeben. Die Standardfunktion gibt den Index des Elements zurück, aber Sie sollten dies nach Möglichkeit überschreiben, um einen eindeutigen Bezeichner für jedes Element über den gesamten Satz zurückzugeben. Diese Funktion sollte memoisiert werden, um unnötige Neu-Renderings zu vermeiden.

### `rangeExtractor`

```tsx
rangeExtractor?: (range: Range) => number[]
```

Diese Funktion erhält sichtbare Bereichsindizes und sollte ein Array von zu rendernden Indizes zurückgeben. Dies ist nützlich, wenn Sie unabhängig vom sichtbaren Bereich manuell Elemente hinzufügen oder entfernen müssen, z.B. für sticky Elemente, Header, Footer usw. Die Standardimplementierung des Range Extractors gibt die sichtbaren Bereichsindizes zurück und ist als `defaultRangeExtractor` exportiert.

### `scrollToFn`

```tsx
scrollToFn?: (
  offset: number,
  options: { adjustments?: number; behavior?: 'auto' | 'smooth' },
  instance: Virtualizer<TScrollElement, TItemElement>,
) => void
```

Eine optionale Funktion, die (falls bereitgestellt) das Scrollverhalten für Ihr ScrollElement implementieren sollte. Sie wird mit folgenden Argumenten aufgerufen:

- Ein `offset` (in Pixeln), zu dem gescrollt werden soll.
- Ein Objekt, das angibt, ob es eine Differenz zwischen der geschätzten Größe und der tatsächlichen Größe gab (`adjustments`) und/oder ob das Scrollen mit einer sanften Animation aufgerufen wurde (`behavior`).
- Die Virtualizer-Instanz selbst.

Hinweis: Integrierte Scroll-Implementierungen sind als `elementScroll` und `windowScroll` exportiert, die automatisch durch die Framework-Adapter-Funktionen wie `useVirtualizer` oder `useWindowVirtualizer` konfiguriert werden.

> ⚠️ Der Versuch, smoothScroll mit dynamisch gemessenen Elementen zu verwenden, funktioniert nicht.

### `observeElementRect`

```tsx
observeElementRect: (
  instance: Virtualizer<TScrollElement, TItemElement>,
  cb: (rect: Rect) => void,
) => void | (() => void)
```

Eine optionale Funktion, die (falls bereitgestellt) aufgerufen wird, wenn sich das ScrollElement ändert, und die initiale Messung und kontinuierliche Überwachung des `Rect` des ScrollElements (ein Objekt mit `width` und `height`) implementieren sollte. Sie wird mit der Instanz aufgerufen (die Ihnen auch Zugriff auf das ScrollElement über `instance.scrollElement` gibt). Integrierte Implementierungen sind als `observeElementRect` und `observeWindowRect` exportiert, die automatisch durch die Framework-Adapter-Funktionen wie `useVirtualizer` oder `useWindowVirtualizer` konfiguriert werden.

### `observeElementOffset`

```tsx
observeElementOffset: (
    instance: Virtualizer<TScrollElement, TItemElement>,
    cb: (offset: number) => void,
  ) => void | (() => void)
```

Eine optionale Funktion, die (falls bereitgestellt) aufgerufen wird, wenn sich das ScrollElement ändert, und die initiale Messung und kontinuierliche Überwachung des Scroll-Offsets des ScrollElements (eine Zahl) implementieren sollte. Sie wird mit der Instanz aufgerufen (die Ihnen auch Zugriff auf das ScrollElement über `instance.scrollElement` gibt). Integrierte Implementierungen sind als `observeElementOffset` und `observeWindowOffset` exportiert, die automatisch durch die Framework-Adapter-Funktionen wie `useVirtualizer` oder `useWindowVirtualizer` konfiguriert werden.

### `measureElement`

```tsx
measureElement?: (
  element: TItemElement,
  entry: ResizeObserverEntry | undefined,
  instance: Virtualizer<TScrollElement, TItemElement>,
) => number
```

Diese optionale Funktion wird aufgerufen, wenn der Virtualizer die Größe (Breite oder Höhe) eines Elements dynamisch messen muss.

> 🧠 Sie können `instance.options.horizontal` verwenden, um zu bestimmen, ob die Breite oder Höhe des Elements gemessen werden soll.

### `scrollMargin`

```tsx
scrollMargin?: number
```

Mit dieser Option können Sie festlegen, wo der Scroll-Offset beginnen soll. Typischerweise repräsentiert dieser Wert den Abstand zwischen dem Anfang des Scroll-Elements und dem Beginn der Liste. Dies ist besonders nützlich in gängigen Szenarien, wie z.B. wenn Sie einen Header vor einem Window-Virtualizer haben oder wenn mehrere Virtualizer innerhalb eines einzigen Scroll-Elements verwendet werden. Wenn Sie absolute Positionierung von Elementen verwenden, sollten Sie den `scrollMargin` in Ihrer CSS-Transform berücksichtigen:
```tsx
transform: `translateY(${
   virtualRow.start - rowVirtualizer.options.scrollMargin
}px)` 
``` 
Um den Wert für `scrollMargin` dynamisch zu messen, können Sie `getBoundingClientRect()` oder ResizeObserver verwenden. Dies ist hilfreich in Szenarien, in denen Elemente über Ihrer virtuellen Liste ihre Höhe ändern können.

### `gap`

```tsx
gap?: number
```

Diese Option ermöglicht es Ihnen, den Abstand zwischen Elementen in der virtualisierten Liste festzulegen. Sie ist besonders nützlich, um eine konsistente visuelle Trennung zwischen Elementen beizubehalten, ohne die Ränder oder Abstände jedes Elements manuell anpassen zu müssen. Der Wert wird in Pixeln angegeben.

### `lanes`

```tsx
lanes: number
```

Die Anzahl der Spuren, in die die Liste unterteilt ist (auch Spalten für vertikale Listen und Zeilen für horizontale Listen).

### `isScrollingResetDelay`

```tsx
isScrollingResetDelay: number
```

Diese Option ermöglicht es Ihnen, die Dauer festzulegen, die nach dem letzten Scroll-Ereignis gewartet werden soll, bevor die isScrolling-Instanzeigenschaft zurückgesetzt wird. Der Standardwert beträgt 150 Millisekunden.

Die Implementierung dieser Option wird durch die Notwendigkeit eines zuverlässigen Mechanismus zur Handhabung des Scrollverhaltens über verschiedene Browser hinweg angetrieben. Bis alle Browser den scrollEnd-Event einheitlich unterstützen.

### `useScrollendEvent`

```tsx
useScrollendEvent: boolean
```

Bestimmt, ob das native scrollend-Event verwendet werden soll, um zu erkennen, wann das Scrollen gestoppt wurde. Wenn auf false gesetzt, wird ein debounced-Fallback verwendet, um die isScrolling-Instanzeigenschaft nach isScrollingResetDelay Millisekunden zurückzusetzen. Der Standardwert ist `false`.

Die Implementierung dieser Option wird durch die Notwendigkeit eines zuverlässigen Mechanismus zur Handhabung des Scrollverhaltens über verschiedene Browser hinweg angetrieben. Bis alle Browser den scrollEnd-Event einheitlich unterstützen.

### `isRtl`

```tsx
isRtl: boolean
```

Ob das horizontale Scrollen invertiert werden soll, um rechts-nach-links-Sprachumgebungen zu unterstützen.

### `useAnimationFrameWithResizeObserver`

```tsx
useAnimationFrameWithResizeObserver: boolean
```

Diese Option aktiviert das Einwickeln von ResizeObserver-Messungen in requestAnimationFrame für flüssigere Updates und weniger Layout-Thrashing. Der Standardwert ist `false`.

Es hilft, den Fehler "ResizeObserver loop completed with undelivered notifications" zu vermeiden, indem sichergestellt wird, dass Messungen mit dem Rendering-Zyklus übereinstimmen. Dies kann die Leistung verbessern und UI-Ruckeln reduzieren, insbesondere wenn Elemente dynamisch in der Größe geändert werden. Da ResizeObserver jedoch bereits asynchron läuft, kann das Hinzufügen von requestAnimationFrame eine leichte Verzögerung bei Messungen verursachen, die in einigen Fällen bemerkbar sein kann. Wenn Größenänderungsoperationen leichtgewichtig sind und keine Reflows verursachen, bietet diese Option möglicherweise keine signifikanten Vorteile.

## Virtualizer-Instanz

Die folgenden Eigenschaften und Methoden sind auf der Virtualizer-Instanz verfügbar:

### `options`

```tsx
options: readonly Required<VirtualizerOptions<TScrollElement, TItemElement>>
```

Die aktuellen Optionen für den Virtualizer. Diese Eigenschaft wird über Ihren Framework-Adapter aktualisiert und ist schreibgeschützt.

### `scrollElement`

```tsx
scrollElement: readonly TScrollElement | null
```

Das aktuelle ScrollElement für den Virtualizer. Diese Eigenschaft wird über Ihren Framework-Adapter aktualisiert und ist schreibgeschützt.

### `getVirtualItems`

```tsx
type getVirtualItems = () => VirtualItem[]
```

Gibt die virtuellen Elemente für den aktuellen Zustand des Virtualizers zurück.

### `getVirtualIndexes`

```tsx
type getVirtualIndexes = () => number[]
```

Gibt die virtuellen Zeilenindizes für den aktuellen Zustand des Virtualizers zurück.

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

Scrollt den Virtualizer zum angegebenen Pixel-Offset. Optional können Sie einen Ausrichtungsmodus übergeben, um den Scroll an einem bestimmten Teil des ScrollElements zu verankern.

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

Scrollt den Virtualizer zu dem Element des angegebenen Index. Optional können Sie einen Ausrichtungsmodus übergeben, um den Scroll an einem bestimmten Teil des ScrollElements zu verankern.

### `getTotalSize`

```tsx
getTotalSize: () => number
```

Gibt die Gesamtgröße in Pixeln für die virtualisierten Elemente zurück. Diese Messung ändert sich inkrementell, wenn Sie sich entscheiden, Ihre Elemente dynamisch zu messen, während sie gerendert werden.

### `measure`

```tsx
measure: () => void
```

Setzt alle vorherigen Elementmessungen zurück.

### `measureElement`

```tsx
measureElement: (el: TItemElement | null) => void
```

Misst das Element mit Ihrer konfigurierten `measureElement`-Virtualizer-Option. Sie sind dafür verantwortlich, dies in Ihrem Virtualizer-Markup aufzurufen, wenn die Komponente gerendert wird (z.B. mit etwas wie Reacts ref-Callback-Prop) und auch `data-index` hinzuzufügen.

```tsx
 <div
  key={virtualRow.key}
  data-index={virtualRow.index}
  ref={virtualizer.measureElement}
  style={...}
>...</div>
```

Standardmäßig ist die `measureElement`-Virtualizer-Option so konfiguriert, dass Elemente mit `getBoundingClientRect()` gemessen werden.

### `resizeItem`

```tsx
resizeItem: (index: number, size: number) => void
```

Ändert die Größe des virtualisierten Elements manuell. Verwenden Sie diese Funktion, um die für diesen Index berechnete Größe manuell festzulegen. Nützlich in Fällen, in denen Sie eine benutzerdefinierte Morphing-Transition verwenden und die Größe des gemorphten Elements im Voraus kennen.

Sie können diese Methode auch mit einem gedrosselten ResizeObserver anstelle von `Virtualizer.measureElement` verwenden, um Neu-Renderings zu reduzieren.

> ⚠️ Bitte beachten Sie, dass das manuelle Ändern der Größe eines Elements, wenn `Virtualizer.measureElement` zur Überwachung dieses Elements verwendet wird, zu unvorhersehbarem Verhalten führt, da `Virtualizer.measureElement` ebenfalls die Größe ändert. Sie können jedoch entweder resizeItem oder measureElement in derselben Virtualizer-Instanz, aber auf verschiedenen Elementindizes verwenden.

### `scrollRect`

```tsx
scrollRect: Rect
```

Aktuelles `Rect` des Scroll-Elements.

### `shouldAdjustScrollPositionOnItemSizeChange`

```tsx
shouldAdjustScrollPositionOnItemSizeChange: undefined | ((item: VirtualItem, delta: number, instance: Virtualizer<TScrollElement, TItemElement>) => boolean)
```

Die shouldAdjustScrollPositionOnItemSizeChange-Methode ermöglicht eine fein abgestimmte Kontrolle über die Anpassung der Scroll-Position, wenn die Größe dynamisch gerenderter Elemente von der geschätzten Größe abweicht. Wenn Sie in die Mitte der Liste springen und rückwärts scrollen, können neue Elemente eine andere Größe als die ursprünglich geschätzte Größe haben. Diese Diskrepanz kann dazu führen, dass nachfolgende Elemente verschoben werden, was insbesondere beim Rückwärts-Scrollen durch die Liste das Nutzererlebnis stören kann.

### `isScrolling`

```tsx
isScrolling: boolean
```

Boolean-Flag, das angibt, ob die Liste gerade gescrollt wird.

### `scrollDirection`

```tsx
scrollDirection: 'forward' | 'backward' | null
```

Diese Option gibt die Scrollrichtung an, mit möglichen Werten 'forward' für das Abwärts-Scrollen und 'backward' für das Aufwärts-Scrollen. Der Wert ist null, wenn kein aktives Scrollen stattfindet.

### `scrollOffset`

```tsx
scrollOffset
