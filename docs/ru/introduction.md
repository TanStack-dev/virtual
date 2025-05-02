---
source-updated-at: '2024-11-25T13:01:52.000Z'
translation-updated-at: '2025-05-02T20:45:20.080Z'
title: Введение
---
TanStack Virtual — это headless-утилита (headless UI utility) для виртуализации длинных списков элементов в JS/TS, React, Vue, Svelte, Solid, Lit и Angular. Это не компонент, поэтому он не предоставляет и не рендерит разметку или стили за вас. Хотя это требует небольшой разметки и стилей с вашей стороны, вы сохраняете 100% контроль над стилями, дизайном и реализацией.

## Виртуализатор (Virtualizer)

В основе TanStack Virtual лежит `Virtualizer`. Виртуализаторы могут быть ориентированы по вертикальной (по умолчанию) или горизонтальной осям, что позволяет достичь вертикальной, горизонтальной и даже грид-подобной виртуализации, комбинируя конфигурации обеих осей.

Вот краткий пример того, как выглядит виртуализация длинного списка внутри div с использованием TanStack Virtual в React:

```tsx
import { useVirtualizer } from '@tanstack/react-virtual';

function App() {
  // Прокручиваемый элемент для вашего списка
  const parentRef = React.useRef(null)

  // Виртуализатор
  const rowVirtualizer = useVirtualizer({
    count: 10000,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 35,
  })

  return (
    <>
      {/* Прокручиваемый элемент для вашего списка */}
      <div
        ref={parentRef}
        style={{
          height: `400px`,
          overflow: 'auto', // Включаем прокрутку!
        }}
      >
        {/* Большой внутренний элемент для хранения всех элементов */}
        <div
          style={{
            height: `${rowVirtualizer.getTotalSize()}px`,
            width: '100%',
            position: 'relative',
          }}
        >
          {/* Только видимые элементы в виртуализаторе, вручную позиционированные для отображения */}
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
              Строка {virtualItem.index}
            </div>
          ))}
        </div>
      </div>
    </>
  )
}
```

Давайте рассмотрим больше примеров!
