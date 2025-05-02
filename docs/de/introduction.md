---
source-updated-at: '2024-11-25T13:01:52.000Z'
translation-updated-at: '2025-05-02T20:38:24.549Z'
title: Einführung
---
TanStack Virtual ist eine Headless-UI-Hilfsfunktion (Headless UI Utility) zur Virtualisierung langer Elementlisten in JS/TS, React, Vue, Svelte, Solid, Lit und Angular. Es handelt sich nicht um eine Komponente, daher liefert es keine Markup-Elemente oder Styles für Sie aus. Obwohl dies etwas Markup und Styles von Ihnen erfordert, behalten Sie zu 100% die Kontrolle über Ihre Styles, Ihr Design und Ihre Implementierung.

## Der Virtualizer

Das Herzstück von TanStack Virtual ist der `Virtualizer`. Virtualizer können entweder vertikal (Standard) oder horizontal ausgerichtet werden, wodurch es möglich ist, vertikale, horizontale und sogar rasterartige Virtualisierung zu erreichen, indem die beiden Achsenkonfigurationen kombiniert werden.

Hier ist ein kurzes Beispiel, wie es aussieht, eine lange Liste innerhalb eines div-Elements mit TanStack Virtual in React zu virtualisieren:

```tsx
import { useVirtualizer } from '@tanstack/react-virtual';

function App() {
  // Das scrollbare Element für Ihre Liste
  const parentRef = React.useRef(null)

  // Der Virtualizer
  const rowVirtualizer = useVirtualizer({
    count: 10000,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 35,
  })

  return (
    <>
      {/* Das scrollbare Element für Ihre Liste */}
      <div
        ref={parentRef}
        style={{
          height: `400px`,
          overflow: 'auto', // Damit es scrollt!
        }}
      >
        {/* Das große innere Element, das alle Items enthält */}
        <div
          style={{
            height: `${rowVirtualizer.getTotalSize()}px`,
            width: '100%',
            position: 'relative',
          }}
        >
          {/* Nur die sichtbaren Items im Virtualizer, manuell positioniert, um sichtbar zu sein */}
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

Lassen Sie uns einige weitere Beispiele genauer betrachten!
