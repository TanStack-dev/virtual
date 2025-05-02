---
source-updated-at: '2024-08-29T09:26:23.000Z'
translation-updated-at: '2025-05-02T20:42:27.650Z'
title: VirtualItem
---
# VirtualItem

L'objet `VirtualItem` représente un élément unique renvoyé par le virtualiseur. Il contient les informations nécessaires pour afficher l'élément dans l'espace de coordonnées du scrollElement de votre virtualiseur, ainsi que d'autres propriétés et fonctions utiles.

```tsx
export interface VirtualItem {
  key: string | number | bigint
  index: number
  start: number
  end: number
  size: number
}
```

Les propriétés et méthodes suivantes sont disponibles sur chaque objet VirtualItem :

### `key`

```tsx
key: string | number | bigint
```

La clé unique de l'élément. Par défaut, il s'agit de l'index de l'élément, mais cela peut être configuré via l'option `getItemKey` du Virtualizer.

### `index`

```tsx
index: number
```

L'index de l'élément.

### `start`

```tsx
start: number
```

Le décalage en pixels du début de l'élément. Cela est généralement mappé à une propriété CSS ou à une transformation comme `top/left` ou `translateX/translateY`.

### `end`

```tsx
end: number
```

Le décalage en pixels de la fin de l'élément. Cette valeur n'est pas nécessaire pour la plupart des mises en page, mais peut être utile, c'est pourquoi nous l'avons incluse.

### `size`

```tsx
size: number
```

La taille de l'élément. Cela est généralement mappé à une propriété CSS comme `width/height`. Avant qu'un élément ne soit mesuré avec la méthode `VirtualItem.measureElement`, cette valeur correspondra à la taille estimée renvoyée par votre option `estimateSize` du virtualiseur. Après la mesure d'un élément (si vous choisissez de le mesurer), cette valeur sera le nombre renvoyé par votre option `measureElement` du virtualiseur (qui par défaut est configurée pour mesurer les éléments avec `getBoundingClientRect()`).

### `lane`

```tsx
lane: number
```

L'index de la ligne (lane) de l'élément. Dans les listes régulières, il sera toujours défini sur `0`, mais devient utile pour les mises en page de type maçonnerie (voir les exemples variables pour plus de détails).
