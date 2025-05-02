---
source-updated-at: '2024-08-29T09:26:23.000Z'
translation-updated-at: '2025-05-02T20:34:11.257Z'
title: Elemento virtual
---
El objeto `VirtualItem` representa un único elemento devuelto por el virtualizador. Contiene la información necesaria para renderizar el elemento en el espacio de coordenadas dentro del `scrollElement` de su virtualizador, junto con otras propiedades/funciones útiles.

```tsx
export interface VirtualItem {
  key: string | number | bigint
  index: number
  start: number
  end: number
  size: number
}
```

Las siguientes propiedades y métodos están disponibles en cada objeto `VirtualItem`:

### `key`

```tsx
key: string | number | bigint
```

La clave única del elemento. Por defecto, corresponde al índice del elemento, pero debe configurarse mediante la opción `getItemKey` del Virtualizador.

### `index`

```tsx
index: number
```

El índice del elemento.

### `start`

```tsx
start: number
```

El desplazamiento en píxeles donde comienza el elemento. Generalmente se asigna a una propiedad CSS o transformación como `top/left` o `translateX/translateY`.

### `end`

```tsx
end: number
```

El desplazamiento en píxeles donde termina el elemento. Este valor no es necesario para la mayoría de los diseños, pero puede ser útil, por lo que se incluye de todas formas.

### `size`

```tsx
size: number
```

El tamaño del elemento. Normalmente se asigna a una propiedad CSS como `width/height`. Antes de que un elemento sea medido con el método `VirtualItem.measureElement`, este valor será el tamaño estimado devuelto por la opción `estimateSize` del virtualizador. Después de medir el elemento (si se elige medirlo), este valor será el número devuelto por la opción `measureElement` del virtualizador (que, por defecto, está configurada para medir elementos con `getBoundingClientRect()`).

### `lane`

```tsx
lane: number
```

El índice del "carril" (lane) del elemento. En listas regulares siempre será `0`, pero resulta útil para diseños de tipo mampostería (consulte los ejemplos variables para más detalles).
