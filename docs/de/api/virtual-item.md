---
source-updated-at: '2024-08-29T09:26:23.000Z'
translation-updated-at: '2025-05-02T20:38:59.662Z'
title: VirtualItem
---
Das `VirtualItem`-Objekt repräsentiert ein einzelnes Element, das vom Virtualisierer zurückgegeben wird. Es enthält die Informationen, die Sie benötigen, um das Element im Koordinatenraum innerhalb des `scrollElement` Ihres Virtualisierers zu rendern, sowie weitere hilfreiche Eigenschaften und Funktionen.

```tsx
export interface VirtualItem {
  key: string | number | bigint
  index: number
  start: number
  end: number
  size: number
}
```

Die folgenden Eigenschaften und Methoden sind für jedes `VirtualItem`-Objekt verfügbar:

### `key`

```tsx
key: string | number | bigint
```

Der eindeutige Schlüssel für das Element. Standardmäßig ist dies der Index des Elements, sollte jedoch über die `getItemKey`-Option des Virtualisierers konfiguriert werden.

### `index`

```tsx
index: number
```

Der Index des Elements.

### `start`

```tsx
start: number
```

Der Start-Pixel-Offset des Elements. Dies wird normalerweise auf eine CSS-Eigenschaft oder Transformation wie `top/left` oder `translateX/translateY` abgebildet.

### `end`

```tsx
end: number
```

Der End-Pixel-Offset des Elements. Dieser Wert ist für die meisten Layouts nicht notwendig, kann aber hilfreich sein, daher wird er trotzdem bereitgestellt.

### `size`

```tsx
size: number
```

Die Größe des Elements. Dies wird normalerweise auf eine CSS-Eigenschaft wie `width/height` abgebildet. Bevor ein Element mit der `VirtualItem.measureElement`-Methode vermessen wird, ist dies die geschätzte Größe, die von der `estimateSize`-Option des Virtualisierers zurückgegeben wird. Nachdem ein Element vermessen wurde (falls Sie es überhaupt vermessen), entspricht dieser Wert der von der `measureElement`-Option des Virtualisierers zurückgegebenen Zahl (die standardmäßig so konfiguriert ist, dass Elemente mit `getBoundingClientRect()` vermessen werden).

### `lane`

```tsx
lane: number
```

Der Lane-Index des Elements. In regulären Listen ist dieser immer auf `0` gesetzt, wird jedoch für Masonry-Layouts nützlich (siehe variable Beispiele für weitere Details).
