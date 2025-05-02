---
source-updated-at: '2024-08-29T09:26:23.000Z'
translation-updated-at: '2025-05-02T20:29:56.520Z'
title: バーチャルアイテム
---
# VirtualItem

`VirtualItem` オブジェクトは、バーチャライザーによって返される単一のアイテムを表します。このオブジェクトには、バーチャライザーの `scrollElement` 内の座標空間でアイテムをレンダリングするために必要な情報や、その他の便利なプロパティ/関数が含まれています。

```tsx
export interface VirtualItem {
  key: string | number | bigint
  index: number
  start: number
  end: number
  size: number
}
```

各 `VirtualItem` オブジェクトで利用可能なプロパティとメソッドは以下の通りです:

### `key`

```tsx
key: string | number | bigint
```

アイテムの一意のキー。デフォルトではアイテムのインデックスですが、`getItemKey` バーチャライザーオプションで設定する必要があります。

### `index`

```tsx
index: number
```

アイテムのインデックス。

### `start`

```tsx
start: number
```

アイテムの開始ピクセルオフセット。通常、`top/left` や `translateX/translateY` などのCSSプロパティやトランスフォームにマッピングされます。

### `end`

```tsx
end: number
```

アイテムの終了ピクセルオフセット。ほとんどのレイアウトではこの値は必要ありませんが、参考のために提供されています。

### `size`

```tsx
size: number
```

アイテムのサイズ。通常、`width/height` などのCSSプロパティにマッピングされます。`VirtualItem.measureElement` メソッドでアイテムが測定される前は、この値は `estimateSize` バーチャライザーオプションから返される推定サイズになります。アイテムが測定された後（測定する場合）は、この値は `measureElement` バーチャライザーオプションから返される値になります（デフォルトでは `getBoundingClientRect()` で要素を測定するように設定されています）。

### `lane`

```tsx
lane: number
```

アイテムのレーンインデックス。通常のリストでは常に `0` に設定されますが、メゾンリーレイアウトでは有用です（詳細は変数例を参照してください）。
