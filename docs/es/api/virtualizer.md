---
source-updated-at: '2025-05-05T15:05:35.000Z'
translation-updated-at: '2025-05-06T23:04:57.546Z'
title: Virtualizador
---
# Virtualizer (no incluir esto en la traducción)

La clase `Virtualizer` es el núcleo de TanStack Virtual. Normalmente, las instancias de Virtualizer son creadas para usted por su adaptador de framework, pero usted recibe directamente el virtualizador.

```tsx
export class Virtualizer<TScrollElement = unknown, TItemElement = unknown> {
  constructor(options: VirtualizerOptions<TScrollElement, TItemElement>)
}
```

## Opciones Requeridas

### `count`

```tsx
count: number
```

El número total de elementos a virtualizar.

### `getScrollElement`

```tsx
getScrollElement: () => TScrollElement
```

Una función que devuelve el elemento desplazable para el virtualizador. Puede devolver null si el elemento aún no está disponible.

### `estimateSize`

```tsx
estimateSize: (index: number) => number
```

> 🧠 Si está midiendo dinámicamente sus elementos, se recomienda estimar el tamaño máximo posible (ancho/alto, dentro de lo razonable) de sus elementos. Esto asegurará que características como el desplazamiento suave tengan más probabilidades de funcionar correctamente.

Esta función recibe el índice de cada elemento y debe devolver el tamaño real (o tamaño estimado si medirá dinámicamente los elementos con `virtualItem.measureElement`) para cada elemento. Esta medida debe devolver el ancho o el alto dependiendo de la orientación de su virtualizador.

## Opciones Opcionales

### `enabled`

```tsx
enabled?: boolean
```

Establézcalo en `false` para desactivar los observadores del scrollElement y reiniciar el estado del virtualizador.

### `debug`

```tsx
debug?: boolean
```

Establézcalo en `true` para habilitar registros de depuración.

### `initialRect`

```tsx
initialRect?: Rect
```

El `Rect` inicial del scrollElement. Esto es principalmente útil si necesita ejecutar el virtualizador en un entorno de Renderizado del lado del servidor (SSR), de lo contrario, el initialRect se calculará al montar mediante la implementación de `observeElementRect`.

### `onChange`

```tsx
onChange?: (instance: Virtualizer<TScrollElement, TItemElement>, sync: boolean) => void
```

Una función de callback que se ejecuta cuando cambia el estado interno del virtualizador. Recibe la instancia del virtualizador y el parámetro sync.

El parámetro sync indica si el desplazamiento está en curso. Es `true` cuando el desplazamiento está en progreso y `false` cuando el desplazamiento se ha detenido o se están realizando otras acciones (como redimensionar).

### `overscan`

```tsx
overscan?: number
```

El número de elementos a renderizar por encima y por debajo del área visible. Aumentar este número incrementará el tiempo que toma renderizar el virtualizador, pero podría disminuir la probabilidad de ver elementos en blanco de renderización lenta en la parte superior e inferior del virtualizador al desplazarse. El valor predeterminado es `1`.

### `horizontal`

```tsx
horizontal?: boolean
```

Establézcalo en `true` si su virtualizador está orientado horizontalmente.

### `paddingStart`

```tsx
paddingStart?: number
```

El relleno a aplicar al inicio del virtualizador en píxeles.

### `paddingEnd`

```tsx
paddingEnd?: number
```

El relleno a aplicar al final del virtualizador en píxeles.

### `scrollPaddingStart`

```tsx
scrollPaddingStart?: number
```

El relleno a aplicar al inicio del virtualizador en píxeles al desplazarse a un elemento.

### `scrollPaddingEnd`

```tsx
scrollPaddingEnd?: number
```

El relleno a aplicar al final del virtualizador en píxeles al desplazarse a un elemento.

### `initialOffset`

```tsx
initialOffset?: number | (() => number)
```

El desplazamiento inicial a aplicar al virtualizador. Esto suele ser útil solo si está renderizando el virtualizador en un entorno de Renderizado del lado del servidor (SSR).

### `getItemKey`

```tsx
getItemKey?: (index: number) => Key
```

Esta función recibe el índice de cada elemento y debe devolver una clave única para ese elemento. La funcionalidad predeterminada de esta función es devolver el índice del elemento, pero debería sobrescribir esto cuando sea posible para devolver un identificador único para cada elemento en todo el conjunto. Esta función debe estar memorizada para evitar re-renderizados innecesarios.

### `rangeExtractor`

```tsx
rangeExtractor?: (range: Range) => number[]
```

Esta función recibe los índices del rango visible y debe devolver un arreglo de índices a renderizar. Esto es útil si necesita agregar o eliminar elementos del virtualizador manualmente independientemente del rango visible, por ejemplo, renderizar elementos fijos, encabezados, pies de página, etc. La implementación predeterminada del extractor de rango devolverá los índices del rango visible y se exporta como `defaultRangeExtractor`.

### `scrollToFn`

```tsx
scrollToFn?: (
  offset: number,
  options: { adjustments?: number; behavior?: 'auto' | 'smooth' },
  instance: Virtualizer<TScrollElement, TItemElement>,
) => void
```

Una función opcional que (si se proporciona) debe implementar el comportamiento de desplazamiento para su scrollElement. Se llamará con los siguientes argumentos:

- Un `offset` (en píxeles) hacia el cual desplazarse.
- Un objeto que indica si hubo una diferencia entre el tamaño estimado y el tamaño real (`adjustments`) y/o si el desplazamiento se llamó con una animación suave (`behavior`).
- La instancia del virtualizador en sí.

Tenga en cuenta que las implementaciones de desplazamiento incorporadas se exportan como `elementScroll` y `windowScroll`, que se configuran automáticamente mediante las funciones del adaptador de framework como `useVirtualizer` o `useWindowVirtualizer`.

> ⚠️ Intentar usar smoothScroll con elementos medidos dinámicamente no funcionará.

### `observeElementRect`

```tsx
observeElementRect: (
  instance: Virtualizer<TScrollElement, TItemElement>,
  cb: (rect: Rect) => void,
) => void | (() => void)
```

Una función opcional que, si se proporciona, se llama cuando cambia el scrollElement y debe implementar la medición inicial y el monitoreo continuo del `Rect` del scrollElement (un objeto con `width` y `height`). Se llama con la instancia (que también le da acceso al scrollElement mediante `instance.scrollElement`). Las implementaciones incorporadas se exportan como `observeElementRect` y `observeWindowRect`, que se configuran automáticamente para usted mediante las funciones exportadas del adaptador de framework como `useVirtualizer` o `useWindowVirtualizer`.

### `observeElementOffset`

```tsx
observeElementOffset: (
    instance: Virtualizer<TScrollElement, TItemElement>,
    cb: (offset: number) => void,
  ) => void | (() => void)
```

Una función opcional que, si se proporciona, se llama cuando cambia el scrollElement y debe implementar la medición inicial y el monitoreo continuo del desplazamiento del scrollElement (un número). Se llama con la instancia (que también le da acceso al scrollElement mediante `instance.scrollElement`). Las implementaciones incorporadas se exportan como `observeElementOffset` y `observeWindowOffset`, que se configuran automáticamente para usted mediante las funciones exportadas del adaptador de framework como `useVirtualizer` o `useWindowVirtualizer`.

### `measureElement`

```tsx
measureElement?: (
  element: TItemElement,
  entry: ResizeObserverEntry | undefined,
  instance: Virtualizer<TScrollElement, TItemElement>,
) => number
```

Esta función opcional se llama cuando el virtualizador necesita medir dinámicamente el tamaño (ancho o alto) de un elemento.

> 🧠 Puede usar `instance.options.horizontal` para determinar si se debe medir el ancho o el alto del elemento.

### `scrollMargin`

```tsx
scrollMargin?: number
```

Con esta opción, puede especificar de dónde debe originarse el desplazamiento. Normalmente, este valor representa el espacio entre el inicio del elemento desplazable y el comienzo de la lista. Esto es especialmente útil en escenarios comunes, como cuando tiene un encabezado antes de un virtualizador de ventana o cuando se utilizan múltiples virtualizadores dentro de un solo elemento desplazable. Si está utilizando posicionamiento absoluto de elementos, debe tener en cuenta el `scrollMargin` en su transformación CSS:
```tsx
transform: `translateY(${
   virtualRow.start - rowVirtualizer.options.scrollMargin
}px)` 
``` 
Para medir dinámicamente el valor de `scrollMargin`, puede usar `getBoundingClientRect()` o ResizeObserver. Esto es útil en escenarios donde los elementos encima de su lista virtual pueden cambiar su altura.

### `gap`

```tsx
gap?: number
```

Esta opción le permite establecer el espacio entre los elementos en la lista virtualizada. Es particularmente útil para mantener una separación visual consistente entre los elementos sin tener que ajustar manualmente el margen o el relleno de cada elemento. El valor se especifica en píxeles.

### `lanes`

```tsx
lanes: number
```

El número de carriles en los que se divide la lista (también conocidos como columnas para listas verticales y filas para listas horizontales).

### `isScrollingResetDelay`

```tsx
isScrollingResetDelay: number
```

Esta opción le permite especificar la duración a esperar después del último evento de desplazamiento antes de reiniciar la propiedad de instancia isScrolling. El valor predeterminado es 150 milisegundos.

La implementación de esta opción está impulsada por la necesidad de un mecanismo confiable para manejar el comportamiento de desplazamiento en diferentes navegadores. Hasta que todos los navegadores admitan uniformemente el evento scrollEnd.

### `useScrollendEvent`

```tsx
useScrollendEvent: boolean
```

Determina si se debe usar el evento nativo scrollend para detectar cuándo se ha detenido el desplazamiento. Si se establece en false, se usa una alternativa con debounce para reiniciar la propiedad de instancia isScrolling después de isScrollingResetDelay milisegundos. El valor predeterminado es `false`.

La implementación de esta opción está impulsada por la necesidad de un mecanismo confiable para manejar el comportamiento de desplazamiento en diferentes navegadores. Hasta que todos los navegadores admitan uniformemente el evento scrollEnd.

### `isRtl`

```tsx
isRtl: boolean
```

Si se debe invertir el desplazamiento horizontal para admitir configuraciones regionales de idioma de derecha a izquierda.

### `useAnimationFrameWithResizeObserver`

```tsx
useAnimationFrameWithResizeObserver: boolean
```

Esta opción habilita el envolver las mediciones de ResizeObserver en requestAnimationFrame para actualizaciones más suaves y menos bloqueos de diseño. El valor predeterminado es `false`.

Ayuda a prevenir el error "ResizeObserver loop completed with undelivered notifications" al asegurar que las mediciones se alineen con el ciclo de renderizado. Esto puede mejorar el rendimiento y reducir el temblor en la interfaz de usuario, especialmente al redimensionar elementos dinámicamente. Sin embargo, dado que ResizeObserver ya se ejecuta de forma asíncrona, agregar requestAnimationFrame puede introducir un ligero retraso en las mediciones, lo que podría ser notable en algunos casos. Si las operaciones de redimensionamiento son ligeras y no causan reflujos, habilitar esta opción puede no proporcionar beneficios significativos.

## Instancia del Virtualizer

Las siguientes propiedades y métodos están disponibles en la instancia del virtualizador:

### `options`

```tsx
options: readonly Required<VirtualizerOptions<TScrollElement, TItemElement>>
```

Las opciones actuales para el virtualizador. Esta propiedad se actualiza mediante su adaptador de framework y es de solo lectura.

### `scrollElement`

```tsx
scrollElement: readonly TScrollElement | null
```

El scrollElement actual para el virtualizador. Esta propiedad se actualiza mediante su adaptador de framework y es de solo lectura.

### `getVirtualItems`

```tsx
type getVirtualItems = () => VirtualItem[]
```

Devuelve los elementos virtuales para el estado actual del virtualizador.

### `getVirtualIndexes`

```tsx
type getVirtualIndexes = () => number[]
```

Devuelve los índices de fila virtual para el estado actual del virtualizador.

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

Desplaza el virtualizador al desplazamiento en píxeles proporcionado. Opcionalmente, puede pasar un modo de alineación para anclar el desplazamiento a una parte específica del scrollElement.

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

Desplaza el virtualizador al elemento del índice proporcionado. Opcionalmente, puede pasar un modo de alineación para anclar el desplazamiento a una parte específica del scrollElement.

### `getTotalSize`

```tsx
getTotalSize: () => number
```

Devuelve el tamaño total en píxeles para los elementos virtualizados. Esta medida cambiará incrementalmente si elige medir dinámicamente sus elementos a medida que se renderizan.

### `measure`

```tsx
measure: () => void
```

Reinicia cualquier medición previa de elementos.

### `measureElement`

```tsx
measureElement: (el: TItemElement | null) => void
```

Mide el elemento usando su opción `measureElement` configurada en el virtualizador. Usted es responsable de llamar a esto en su marcado del virtualizador cuando el componente se renderiza (por ejemplo, usando algo como la propiedad de callback ref de React) y también agregando `data-index`

```tsx
 <div
  key={virtualRow.key}
  data-index={virtualRow.index}
  ref={virtualizer.measureElement}
  style={...}
>...</div>
```

Por defecto, la opción `measureElement` del virtualizador está configurada para medir elementos con `getBoundingClientRect()`.

### `resizeItem`

```tsx
resizeItem: (index: number, size: number) => void
```

Cambia manualmente el tamaño del elemento virtualizado. Use esta función para establecer manualmente el tamaño calculado para este índice. Útil en ocasiones cuando se usa alguna transición de transformación personalizada y conoce el tamaño del elemento transformado de antemano.

También puede usar este método con un ResizeObserver limitado en lugar de `Virtualizer.measureElement` para reducir los re-renderizados.

> ⚠️ Tenga en cuenta que cambiar manualmente el tamaño de un elemento cuando usa `Virtualizer.measureElement` para monitorear ese elemento resultará en un comportamiento impredecible, ya que `Virtualizer.measureElement` también está cambiando el tamaño. Sin embargo, puede usar uno de resizeItem o measureElement en la misma instancia de virtualizador pero en diferentes índices de elementos.

### `scrollRect`

```tsx
scrollRect: Rect
```

`Rect` actual del elemento de desplazamiento.

### `shouldAdjustScrollPositionOnItemSizeChange`

```tsx
shouldAdjustScrollPositionOnItemSizeChange: undefined | ((item: VirtualItem, delta: number, instance: Virtualizer<TScrollElement, TItemElement>) => boolean)
```

El método shouldAdjustScrollPositionOnItemSizeChange permite un control detallado sobre el ajuste de la posición de desplazamiento cuando el tamaño de los elementos renderizados dinámicamente difiere del tamaño estimado. Al saltar en medio de la lista y desplazarse hacia atrás, los nuevos elementos pueden tener un tamaño diferente al tamaño estimado inicialmente. Esta discrepancia puede hacer que los elementos subsiguientes se desplacen, lo que podría interrumpir la experiencia de desplazamiento del usuario, especialmente al navegar hacia atrás en la lista.

### `isScrolling`

```tsx
isScrolling: boolean
```

Bandera booleana que indica si la lista se está desplazando actualmente.

### `scrollDirection`

```tsx
scrollDirection: 'forward' | 'backward' | null
```

Esta opción indica la dirección del desplazamiento, con posibles valores 'forward' para desplazarse hacia abajo y 'backward' para desplazarse hacia arriba. El valor se establece en null cuando no hay un desplazamiento activo.

### `scrollOffset`

```tsx
scrollOffset: number
```

Esta opción representa la posición actual de desplazamiento a lo largo del eje de desplazamiento. Se mide en píxeles desde el punto de inicio del área desplazable.
