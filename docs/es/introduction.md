---
source-updated-at: '2024-11-25T13:01:52.000Z'
translation-updated-at: '2025-05-02T20:33:34.311Z'
title: Introducción
---
# Introducción

TanStack Virtual es una utilidad de interfaz de usuario sin cabeza (headless UI) para virtualizar listas largas de elementos en JS/TS, React, Vue, Svelte, Solid, Lit y Angular. No es un componente, por lo tanto no incluye ni renderiza ningún marcado o estilos por usted. Si bien esto requiere un poco de marcado y estilos de su parte, usted conservará el 100% de control sobre sus estilos, diseño e implementación.

## El Virtualizador

En el núcleo de TanStack Virtual se encuentra el `Virtualizer`. Los virtualizadores pueden orientarse en los ejes vertical (predeterminado) u horizontal, lo que hace posible lograr virtualización vertical, horizontal e incluso similar a una cuadrícula al combinar las dos configuraciones de ejes.

Aquí hay un ejemplo rápido de cómo se ve la virtualización de una lista larga dentro de un div usando TanStack Virtual en React:

```tsx
import { useVirtualizer } from '@tanstack/react-virtual';

function App() {
  // The scrollable element for your list
  const parentRef = React.useRef(null)

  // The virtualizer
  const rowVirtualizer = useVirtualizer({
    count: 10000,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 35,
  })

  return (
    <>
      {/* The scrollable element for your list */}
      <div
        ref={parentRef}
        style={{
          height: `400px`,
          overflow: 'auto', // Make it scroll!
        }}
      >
        {/* The large inner element to hold all of the items */}
        <div
          style={{
            height: `${rowVirtualizer.getTotalSize()}px`,
            width: '100%',
            position: 'relative',
          }}
        >
          {/* Only the visible items in the virtualizer, manually positioned to be in view */}
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

¡Profundicemos en más ejemplos!
