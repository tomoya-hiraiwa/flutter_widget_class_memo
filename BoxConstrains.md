# BoxConstraints

## 概要
`BoxConstraints` は、Flutter のレイアウトシステムで **ウィジェットのサイズ制約** を定義するためのクラス。`ConstrainedBox` や `SizedBox` などのウィジェットと組み合わせて使用し、最小・最大の幅や高さを設定できる。

## 基本的な使い方
```dart
BoxConstraints(
  minWidth: 50,
  maxWidth: 200,
  minHeight: 100,
  maxHeight: 300,
);
```

## プロパティ
| プロパティ          | 説明 |
|------------------|---------------------------|
| `minWidth`      | 最小幅を指定する（デフォルトは `0`） |
| `maxWidth`      | 最大幅を指定する（デフォルトは `double.infinity`） |
| `minHeight`     | 最小高さを指定する（デフォルトは `0`） |
| `maxHeight`     | 最大高さを指定する（デフォルトは `double.infinity`） |

## `BoxConstraints` を使った例

### 1. `ConstrainedBox` で制約を適用
```dart
ConstrainedBox(
  constraints: BoxConstraints(
    minWidth: 100,
    maxWidth: 300,
    minHeight: 50,
    maxHeight: 150,
  ),
  child: Container(
    color: Colors.blue,
    width: 400,
    height: 200,
  ),
);
```

## 便利なコンストラクタ
| コンストラクタ  | 説明 |
|--------------|----------------------|
| `BoxConstraints.tight(Size size)` | 幅・高さを **固定** する制約を作成 |
| `BoxConstraints.tightFor({double? width, double? height})` | 指定した幅・高さのみ固定する制約 |
| `BoxConstraints.expand({double? width, double? height})` | 親ウィジェットいっぱいに広がる制約 |
| `BoxConstraints.loose(Size size)` | 指定サイズを最大値とする制約 |

### 2. `tight()` で完全固定
```dart
ConstrainedBox(
  constraints: BoxConstraints.tight(Size(150, 100)),
  child: Container(color: Colors.red),
);
```

### 3. `expand()` で親要素いっぱいに広げる
```dart
Container(
  constraints: BoxConstraints.expand(),
  color: Colors.green,
);
```

### 4. `loose()` で最大サイズのみ制限
```dart
ConstrainedBox(
  constraints: BoxConstraints.loose(Size(200, 300)),
  child: Text('Flutter'),
);
```

## `BoxConstraints` のチェックメソッド
| メソッド               | 返り値 | 説明 |
|---------------------|-------|------------------------------|
| `hasBoundedWidth`  | `bool` | `maxWidth < infinity` の場合 `true` |
| `hasBoundedHeight` | `bool` | `maxHeight < infinity` の場合 `true` |
| `isTight`          | `bool` | `minWidth == maxWidth` かつ `minHeight == maxHeight` なら `true` |
| `isSatisfiedBy(Size size)` | `bool` | 指定した `Size` が制約内なら `true` |

## まとめ
- `BoxConstraints` は **ウィジェットのサイズ制約** を定義するクラス。
- `minWidth`, `maxWidth`, `minHeight`, `maxHeight` を指定可能。
- `ConstrainedBox` や `SizedBox` などで活用できる。
- `tight()` は完全固定、`expand()` は親ウィジェットいっぱいに広げる、`loose()` は最大サイズのみ制限する。

