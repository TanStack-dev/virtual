---
source-updated-at: '2025-03-13T14:46:17.000Z'
translation-updated-at: '2025-05-02T20:44:38.365Z'
title: Virtualizer
---
# Virtualizer

La classe `Virtualizer` est au cœur de TanStack Virtual. Les instances de Virtualizer sont généralement créées pour vous par l'adaptateur de votre framework, mais vous recevez directement le virtualizer.

```tsx
export class Virtualizer<TScrollElement = unknown, TItemElement = unknown> {
  constructor(options: VirtualizerOptions<TScrollElement, TItemElement>)
}
```

## Options requises

### `count`

```tsx
count: number
```

Le nombre total d'éléments à virtualiser.

### `getScrollElement`

```tsx
getScrollElement: () => TScrollElement
```

Une fonction qui retourne l'élément scrollable pour le virtualizer. Elle peut retourner null si l'élément n'est pas encore disponible.

### `estimateSize`

```tsx
estimateSize: (index: number) => number
```

> 🧠 Si vous mesurez dynamiquement vos éléments, il est recommandé d'estimer la taille maximale possible (largeur/hauteur, dans une limite raisonnable) de vos éléments. Cela garantira que des fonctionnalités comme le défilement fluide auront plus de chances de fonctionner correctement.

Cette fonction reçoit l'index de chaque élément et doit retourner la taille réelle (ou estimée si vous mesurez dynamiquement les éléments avec `virtualItem.measureElement`) pour chaque élément. Cette mesure doit retourner soit la largeur soit la hauteur selon l'orientation de votre virtualizer.

## Options optionnelles

### `enabled`

```tsx
enabled?: boolean
```

Définissez à `false` pour désactiver les observateurs de scrollElement et réinitialiser l'état du virtualizer.

### `debug`

```tsx
debug?: boolean
```

Définissez à `true` pour activer les logs de débogage.

### `initialRect`

```tsx
initialRect?: Rect
```

Le `Rect` initial du scrollElement. Ceci est surtout utile si vous avez besoin d'exécuter le virtualizer dans un environnement SSR (Server-Side Rendering), sinon le initialRect sera calculé au montage par l'implémentation de `observeElementRect`.

### `onChange`

```tsx
onChange?: (instance: Virtualizer<TScrollElement, TItemElement>, sync: boolean) => void
```

Une fonction de rappel qui se déclenche lorsque l'état interne du virtualizer change. Elle reçoit l'instance du virtualizer et le paramètre sync.

Le paramètre sync indique si un défilement est en cours. Il est à `true` lorsque le défilement est en cours, et `false` lorsque le défilement s'est arrêté ou que d'autres actions (comme un redimensionnement) sont effectuées.

### `overscan`

```tsx
overscan?: number
```

Le nombre d'éléments à rendre au-dessus et en dessous de la zone visible. Augmenter ce nombre augmentera le temps nécessaire pour rendre le virtualizer, mais pourrait réduire la probabilité de voir des éléments vides à rendu lent en haut et en bas du virtualizer lors du défilement.

### `horizontal`

```tsx
horizontal?: boolean
```

Définissez ceci à `true` si votre virtualizer est orienté horizontalement.

### `paddingStart`

```tsx
paddingStart?: number
```

Le padding à appliquer au début du virtualizer en pixels.

### `paddingEnd`

```tsx
paddingEnd?: number
```

Le padding à appliquer à la fin du virtualizer en pixels.

### `scrollPaddingStart`

```tsx
scrollPaddingStart?: number
```

Le padding à appliquer au début du virtualizer en pixels lors du défilement vers un élément.

### `scrollPaddingEnd`

```tsx
scrollPaddingEnd?: number
```

Le padding à appliquer à la fin du virtualizer en pixels lors du défilement vers un élément.

### `initialOffset`

```tsx
initialOffset?: number | (() => number)
```

Le décalage initial à appliquer au virtualizer. Ceci n'est généralement utile que si vous rendez le virtualizer dans un environnement SSR.

### `getItemKey`

```tsx
getItemKey?: (index: number) => Key
```

Cette fonction reçoit l'index de chaque élément et doit retourner une clé unique pour cet élément. La fonctionnalité par défaut de cette fonction est de retourner l'index de l'élément, mais vous devriez la remplacer si possible pour retourner un identifiant unique pour chaque élément dans l'ensemble complet. Cette fonction devrait être mémoïsée pour éviter des rendus inutiles.

### `rangeExtractor`

```tsx
rangeExtractor?: (range: Range) => number[]
```

Cette fonction reçoit les index de la plage visible et doit retourner un tableau d'index à rendre. Ceci est utile si vous avez besoin d'ajouter ou de supprimer des éléments du virtualizer manuellement indépendamment de la plage visible, par exemple pour rendre des éléments fixes, des en-têtes, des pieds de page, etc. L'implémentation par défaut de l'extracteur de plage retournera les index de la plage visible et est exportée sous le nom `defaultRangeExtractor`.

### `scrollToFn`

```tsx
scrollToFn?: (
  offset: number,
  options: { adjustments?: number; behavior?: 'auto' | 'smooth' },
  instance: Virtualizer<TScrollElement, TItemElement>,
) => void
```

Une fonction optionnelle qui (si fournie) doit implémenter le comportement de défilement pour votre scrollElement. Elle sera appelée avec les arguments suivants :

- Un `offset` (en pixels) vers lequel faire défiler.
- Un objet indiquant s'il y a eu une différence entre la taille estimée et la taille réelle (`adjustments`) et/ou si le défilement a été appelé avec une animation fluide (`behavior`).
- L'instance du virtualizer elle-même.

Notez que les implémentations de défilement intégrées sont exportées sous les noms `elementScroll` et `windowScroll`, qui sont automatiquement configurées par les fonctions d'adaptateur de framework comme `useVirtualizer` ou `useWindowVirtualizer`.

> ⚠️ Tenter d'utiliser smoothScroll avec des éléments mesurés dynamiquement ne fonctionnera pas.

### `observeElementRect`

```tsx
observeElementRect: (
  instance: Virtualizer<TScrollElement, TItemElement>,
  cb: (rect: Rect) => void,
) => void | (() => void)
```

Une fonction optionnelle qui, si fournie, est appelée lorsque le scrollElement change et doit implémenter la mesure initiale et la surveillance continue du `Rect` du scrollElement (un objet avec `width` et `height`). Elle est appelée avec l'instance (qui vous donne également accès au scrollElement via `instance.scrollElement`). Les implémentations intégrées sont exportées sous les noms `observeElementRect` et `observeWindowRect` qui sont automatiquement configurées pour vous par les fonctions exportées de votre adaptateur de framework comme `useVirtualizer` ou `useWindowVirtualizer`.

### `observeElementOffset`

```tsx
observeElementOffset: (
    instance: Virtualizer<TScrollElement, TItemElement>,
    cb: (offset: number) => void,
  ) => void | (() => void)
```

Une fonction optionnelle qui, si fournie, est appelée lorsque le scrollElement change et doit implémenter la mesure initiale et la surveillance continue du décalage de défilement du scrollElement (un nombre). Elle est appelée avec l'instance (qui vous donne également accès au scrollElement via `instance.scrollElement`). Les implémentations intégrées sont exportées sous les noms `observeElementOffset` et `observeWindowOffset` qui sont automatiquement configurées pour vous par les fonctions exportées de votre adaptateur de framework comme `useVirtualizer` ou `useWindowVirtualizer`.

### `measureElement`

```tsx
measureElement?: (
  element: TItemElement,
  entry: ResizeObserverEntry | undefined,
  instance: Virtualizer<TScrollElement, TItemElement>,
) => number
```

Cette fonction optionnelle est appelée lorsque le virtualizer a besoin de mesurer dynamiquement la taille (largeur ou hauteur) d'un élément.

> 🧠 Vous pouvez utiliser `instance.options.horizontal` pour déterminer si la largeur ou la hauteur de l'élément doit être mesurée.

### `scrollMargin`

```tsx
scrollMargin?: number
```

Avec cette option, vous pouvez spécifier d'où doit provenir le décalage de défilement. Typiquement, cette valeur représente l'espace entre le début de l'élément de défilement et le début de la liste. Ceci est particulièrement utile dans des scénarios courants comme lorsque vous avez un en-tête précédant un virtualizer de fenêtre ou lorsque plusieurs virtualizers sont utilisés dans un seul élément de défilement. Si vous utilisez le positionnement absolu des éléments, vous devez prendre en compte le `scrollMargin` dans votre transformation CSS :
```tsx
transform: `translateY(${
   virtualRow.start - rowVirtualizer.options.scrollMargin
}px)` 
``` 
Pour mesurer dynamiquement la valeur de `scrollMargin`, vous pouvez utiliser `getBoundingClientRect()` ou ResizeObserver. Ceci est utile dans les scénarios où les éléments au-dessus de votre liste virtuelle pourraient changer de hauteur.

### `gap`

```tsx
gap?: number
```

Cette option vous permet de définir l'espacement entre les éléments de la liste virtualisée. Elle est particulièrement utile pour maintenir une séparation visuelle cohérente entre les éléments sans avoir à ajuster manuellement la marge ou le padding de chaque élément. La valeur est spécifiée en pixels.

### `lanes`

```tsx
lanes: number
```

Le nombre de voies dans lesquelles la liste est divisée (également appelées colonnes pour les listes verticales et lignes pour les listes horizontales).

### `isScrollingResetDelay`

```tsx
isScrollingResetDelay: number
```

Cette option vous permet de spécifier la durée à attendre après le dernier événement de défilement avant de réinitialiser la propriété d'instance isScrolling. La valeur par défaut est 150 millisecondes.

L'implémentation de cette option est motivée par le besoin d'un mécanisme fiable pour gérer le comportement de défilement sur différents navigateurs. Jusqu'à ce que tous les navigateurs prennent en charge uniformément l'événement scrollEnd.

### `useScrollendEvent`

```tsx
useScrollendEvent: boolean
```

Détermine s'il faut utiliser l'événement natif scrollend pour détecter quand le défilement s'est arrêté. Si défini à false, une solution de repli avec debounce est utilisée pour réinitialiser la propriété d'instance isScrolling après isScrollingResetDelay millisecondes. La valeur par défaut est `false`.

L'implémentation de cette option est motivée par le besoin d'un mécanisme fiable pour gérer le comportement de défilement sur différents navigateurs. Jusqu'à ce que tous les navigateurs prennent en charge uniformément l'événement scrollEnd.

### `isRtl`

```tsx
isRtl: boolean
```

Détermine s'il faut inverser le défilement horizontal pour prendre en charge les locales de langue droite-à-gauche.

### `useAnimationFrameWithResizeObserver`

```tsx
useAnimationFrameWithResizeObserver: boolean
```

Cette option permet d'encapsuler les mesures de ResizeObserver dans requestAnimationFrame pour des mises à jour plus fluides et une réduction des conflits de layout. La valeur par défaut est `false`.

Elle aide à prévenir l'erreur "ResizeObserver loop completed with undelivered notifications" en s'assurant que les mesures s'alignent avec le cycle de rendu. Cela peut améliorer les performances et réduire les saccades de l'interface, surtout lors du redimensionnement dynamique des éléments. Cependant, comme ResizeObserver s'exécute déjà de manière asynchrone, l'ajout de requestAnimationFrame peut introduire un léger délai dans les mesures, qui pourrait être perceptible dans certains cas. Si les opérations de redimensionnement sont légères et ne provoquent pas de reflows, activer cette option peut ne pas apporter d'avantages significatifs.

## Instance de Virtualizer

Les propriétés et méthodes suivantes sont disponibles sur l'instance du virtualizer :

### `options`

```tsx
options: readonly Required<VirtualizerOptions<TScrollElement, TItemElement>>
```

Les options actuelles pour le virtualizer. Cette propriété est mise à jour via votre adaptateur de framework et est en lecture seule.

### `scrollElement`

```tsx
scrollElement: readonly TScrollElement | null
```

Le scrollElement actuel pour le virtualizer. Cette propriété est mise à jour via votre adaptateur de framework et est en lecture seule.

### `getVirtualItems`

```tsx
type getVirtualItems = () => VirtualItem[]
```

Retourne les éléments virtuels pour l'état actuel du virtualizer.

### `getVirtualIndexes`

```tsx
type getVirtualIndexes = () => number[]
```

Retourne les index des lignes virtuelles pour l'état actuel du virtualizer.

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

Fait défiler le virtualizer jusqu'au décalage en pixels fourni. Vous pouvez optionnellement passer un mode d'alignement pour ancrer le défilement à une partie spécifique du scrollElement.

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

Fait défiler le virtualizer jusqu'à l'élément de l'index fourni. Vous pouvez optionnellement passer un mode d'alignement pour ancrer le défilement à une partie spécifique du scrollElement.

### `getTotalSize`

```tsx
getTotalSize: () => number
```

Retourne la taille totale en pixels pour les éléments virtualisés. Cette mesure changera progressivement si vous choisissez de mesurer dynamiquement vos éléments lors de leur rendu.

### `measure`

```tsx
measure: () => void
```

Réinitialise toutes les mesures précédentes des éléments.

### `measureElement`

```tsx
measureElement: (el: TItemElement | null) => void
```

Mesure l'élément en utilisant votre option `measureElement` configurée pour le virtualizer. Vous êtes responsable d'appeler ceci dans votre balisage de virtualizer lorsque le composant est rendu (par exemple en utilisant quelque chose comme la prop de rappel ref de React) en ajoutant également `data-index`

```tsx
 <div
  key={virtualRow.key}
  data-index={virtualRow.index}
  ref={virtualizer.measureElement}
  style={...}
>...</div>
```

Par défaut, l'option `measureElement` du virtualizer est configurée pour mesurer les éléments avec `getBoundingClientRect()`.

### `resizeItem`

```tsx
resizeItem: (index: number, size: number) => void
```

Change manuellement la taille de l'élément virtualisé. Utilisez cette fonction pour définir manuellement la taille calculée pour cet index. Utile dans les cas où vous utilisez une transition de morphing personnalisée et que vous connaissez à l'avance la taille de l'élément morphé.

Vous pouvez également utiliser cette méthode avec un ResizeObserver limité au lieu de `Virtualizer.measureElement` pour réduire le re-rendu.

> ⚠️ Soyez conscient que changer manuellement la taille d'un élément lors de l'utilisation de `Virtualizer.measureElement` pour surveiller cet élément entraînera un comportement imprévisible car `Virtualizer.measureElement` modifie également la taille. Cependant, vous pouvez utiliser l'une des méthodes resizeItem ou measureElement dans la même instance de virtualizer mais sur des index d'éléments différents.

### `scrollRect`

```tsx
scrollRect: Rect
```

`Rect` actuel de l'élément de défilement.

### `shouldAdjustScrollPositionOnItemSizeChange`

```tsx
shouldAdjustScrollPositionOnItemSizeChange: undefined | ((item: VirtualItem, delta: number, instance: Virtualizer<TScrollElement, TItemElement>) => boolean)
```

La méthode shouldAdjustScrollPositionOnItemSizeChange permet un contrôle précis de l'ajustement de la position de défilement lorsque la taille des éléments rendus dynamiquement diffère de la taille estimée. Lors d'un saut au milieu de la liste et d'un défilement vers l'arrière, les nouveaux éléments peuvent avoir une taille différente de la taille initialement estimée. Cette divergence peut provoquer un décalage des éléments suivants, perturbant potentiellement l'expérience de défilement de l'utilisateur, en particulier lors de la navigation vers l'arrière dans la liste.

### `isScrolling`

```tsx
isScrolling: boolean
```

Drapeau booléen indiquant si la liste est actuellement en cours de défilement.

### `scrollDirection`

```tsx
scrollDirection: 'forward' | 'backward' | null
```

Cette option indique la direction du défilement, avec les valeurs possibles 'forward' pour un défilement vers le bas et 'backward' pour un défilement vers le haut. La valeur est définie à null lorsqu'il n'y a pas de défilement actif.

### `scrollOffset`

```tsx
scrollOffset: number
```

Cette option représente la position actuelle de défilement le long de l'axe de défilement. Elle est mesurée en pixels à partir du point de départ de la zone défilable.
