---
source-updated-at: '2024-11-25T13:01:52.000Z'
translation-updated-at: '2025-05-02T20:42:06.258Z'
title: Introduction
---
TanStack Virtual est une utilitaire d'interface sans interface prédéfinie (headless UI) pour virtualiser de longues listes d'éléments en JS/TS, React, Vue, Svelte, Solid, Lit et Angular. Ce n'est pas un composant et ne fournit donc aucun balisage (markup) ou style pour vous. Bien que cela nécessite un peu de balisage et de styles de votre part, vous conservez un contrôle à 100 % sur vos styles, votre design et votre implémentation.

## Le Virtualizer

Au cœur de TanStack Virtual se trouve le `Virtualizer`. Les virtualiseurs peuvent être orientés sur les axes vertical (par défaut) ou horizontal, ce qui permet d'atteindre une virtualisation verticale, horizontale et même sous forme de grille en combinant les deux configurations d'axes.

Voici un exemple rapide de ce à quoi ressemble la virtualisation d'une longue liste dans une div en utilisant TanStack Virtual avec React :

```tsx
import { useVirtualizer } from '@tanstack/react-virtual';

function App() {
  // L'élément scrollable pour votre liste
  const parentRef = React.useRef(null)

  // Le virtualiseur
  const rowVirtualizer = useVirtualizer({
    count: 10000,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 35,
  })

  return (
    <>
      {/* L'élément scrollable pour votre liste */}
      <div
        ref={parentRef}
        style={{
          height: `400px`,
          overflow: 'auto', // Permet le défilement !
        }}
      >
        {/* Le grand élément intérieur pour contenir tous les éléments */}
        <div
          style={{
            height: `${rowVirtualizer.getTotalSize()}px`,
            width: '100%',
            position: 'relative',
          }}
        >
          {/* Seuls les éléments visibles dans le virtualiseur, positionnés manuellement pour être visibles */}
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
              Ligne {virtualItem.index}
            </div>
          ))}
        </div>
      </div>
    </>
  )
}
```

Explorons maintenant quelques exemples supplémentaires !
