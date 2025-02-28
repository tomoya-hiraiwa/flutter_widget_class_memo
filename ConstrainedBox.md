# ConstrainedBox

## 概要
`ConstrainedBox` は、子ウィジェットにサイズ制約を適用するためのウィジェット。 `BoxConstraints` を使用して、最小・最大の幅や高さを設定できる。

## 基本的な使い方
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('ConstrainedBox Example')),
        body: Center(
          child: ConstrainedBox(
            constraints: BoxConstraints(
              minWidth: 100,
              maxWidth: 200,
              minHeight: 50,
              maxHeight: 100,
            ),
            child: Container(
              color: Colors.blue,
              width: 250,  // ここで指定した値より小さくなる
              height: 150, // ここで指定した値より小さくなる
            ),
          ),
        ),
      ),
    );
  }
}
```

## 主な用途

### 1. 最小サイズの設定
```dart
ConstrainedBox(
  constraints: BoxConstraints(minWidth: 100, minHeight: 100),
  child: Text('Hello', style: TextStyle(fontSize: 20)),
);
```
**→ `Text` ウィジェットは通常小さいが、最小サイズ `100x100` に拡張される。**

### 2. 無限の制約を防ぐ
`ListView` や `Column` の子ウィジェットに `double.infinity` を設定するとエラーが出ることがある。その場合、`ConstrainedBox` で制限をかけるとエラーを防ぐことができる。

```dart
Expanded(
  child: ConstrainedBox(
    constraints: BoxConstraints(maxHeight: 300),
    child: ListView(
      children: List.generate(20, (index) => ListTile(title: Text('Item $index'))),
    ),
  ),
);
```

## `SizedBox` との違い
| 特性            | `ConstrainedBox`                     | `SizedBox`                   |
|---------------|--------------------------------|-----------------------------|
| サイズ制限     | **最小・最大**のサイズを指定可能 | **固定サイズ**を指定       |
| 動的な変更     | 可能（最小・最大で範囲を調整）  | 不可能（サイズ固定）       |
| 用途           | **柔軟なサイズ制限**が必要な場合 | **完全に固定**したい場合 |

例えば、`SizedBox(width: 100, height: 100)` は **完全に100x100に固定** されるが、  
`ConstrainedBox(constraints: BoxConstraints(minWidth: 100, maxWidth: 200))` は、**範囲内でサイズが変動** する。

## まとめ
- `ConstrainedBox` は **子ウィジェットのサイズを制限** するために使用できる。
- `BoxConstraints` を使って **最小・最大の幅と高さを設定** できる。
- `SizedBox` は固定サイズだが、`ConstrainedBox` は **制約範囲内で調整可能**。
- `ListView` や `Column` の中で `double.infinity` を防ぐ用途にも使える。



