# Stack

## 概要
`Stack` は **ウィジェットを重ねて配置** するためのレイアウトウィジェット。`children` に複数のウィジェットを指定すると、**最初の子ウィジェットが一番下のレイヤー** に、その上に順番に積み重ねられる。

## 基本的な使い方
```dart
Stack(
  children: [
    Container(width: 200, height: 200, color: Colors.blue), // 背景
    Positioned(
      left: 50,
      top: 50,
      child: Container(width: 100, height: 100, color: Colors.red), // 前面
    ),
  ],
)
```

## プロパティ
| プロパティ         | 説明 |
|-----------------|---------------------------|
| `alignment`    | 子ウィジェットの **配置方法** を決定（デフォルト `topLeft`） |
| `clipBehavior` | **範囲外の描画** をクリップするかどうか |
| `fit`         | `StackFit.loose`（デフォルト）や `StackFit.expand` など、子のサイズ指定方式 |

## `alignment` を使った配置
```dart
Stack(
  alignment: Alignment.center,
  children: [
    Container(width: 200, height: 200, color: Colors.green),
    Container(width: 100, height: 100, color: Colors.orange),
  ],
)
```

## `Positioned` でカスタム配置
```dart
Stack(
  children: [
    Container(width: 200, height: 200, color: Colors.grey),
    Positioned(
      left: 20,
      top: 30,
      child: Container(width: 50, height: 50, color: Colors.red),
    ),
  ],
)
```

## `Stack` の `fit` プロパティ
| プロパティ              | 説明 |
|----------------------|---------------------------|
| `StackFit.loose`    | **デフォルト**。子のサイズに従う |
| `StackFit.expand`   | 親ウィジェットのサイズいっぱいに広げる |
| `StackFit.passthrough` | 親ウィジェットの制約を子に渡す |

## `Stack` のクリッピング
```dart
Stack(
  clipBehavior: Clip.hardEdge,
  children: [
    Container(width: 200, height: 200, color: Colors.blue),
    Positioned(
      left: 180,
      child: Container(width: 50, height: 50, color: Colors.red),
    ),
  ],
)
```

## まとめ
- `Stack` は **ウィジェットを重ねて配置** できる。
- `alignment` で **全体の子ウィジェットの位置** を調整可能。
- `Positioned` を使うと **個別に配置** できる。
- `fit` を `expand` にすると **親のサイズいっぱいに広げられる**。
- `clipBehavior` で **はみ出し部分をカット** できる。

