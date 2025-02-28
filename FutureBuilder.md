# FutureBuilder

## 概要
`FutureBuilder` は **非同期処理の結果に応じて UI を構築する** ウィジェット。`Future<T>` の状態に応じて、適切な UI を描画できる。

## 基本的な使い方
```dart
FutureBuilder<String>(
  future: fetchData(), // 非同期処理
  builder: (context, snapshot) {
    if (snapshot.connectionState == ConnectionState.waiting) {
      return CircularProgressIndicator(); // 読み込み中
    } else if (snapshot.hasError) {
      return Text('エラー: ${snapshot.error}'); // エラー発生時
    } else {
      return Text('データ: ${snapshot.data}'); // データ取得成功
    }
  },
);
```

## プロパティ
| プロパティ      | 説明 |
|--------------|---------------------------|
| `future`     | 実行する **非同期処理 (`Future<T>`)** |
| `builder`    | `snapshot` の状態を見ながら **UI を構築する関数** |

## `snapshot` のプロパティ
| プロパティ                 | 説明 |
|-------------------------|---------------------------|
| `connectionState`      | `Future` の現在の状態 |
| `data`                 | `Future` の **成功時の値** |
| `hasData`              | `data` が `null` 以外なら `true` |
| `error`                | `Future` の **エラー内容** |
| `hasError`             | `error` が `null` 以外なら `true` |

## `connectionState` の状態
| `ConnectionState` | 説明 |
|-----------------|----------------------------|
| `none`         | `future` が `null` の場合 |
| `waiting`      | 非同期処理の **実行中** |
| `active`       | `Stream` の場合のみ使用される（`Future` では使われない） |
| `done`         | 非同期処理が **完了した状態** |

## 実装例
### 1. API からデータを取得
```dart
Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2));
  return "取得したデータ";
}

FutureBuilder<String>(
  future: fetchData(),
  builder: (context, snapshot) {
    if (snapshot.connectionState == ConnectionState.waiting) {
      return CircularProgressIndicator();
    } else if (snapshot.hasError) {
      return Text('エラー: ${snapshot.error}');
    } else {
      return Text('データ: ${snapshot.data}');
    }
  },
);
```

### 2. ボタンを押したらデータ取得
```dart
class MyButtonWidget extends StatefulWidget {
  @override
  _MyButtonWidgetState createState() => _MyButtonWidgetState();
}

class _MyButtonWidgetState extends State<MyButtonWidget> {
  Future<String>? _future;

  void _fetchData() {
    setState(() {
      _future = fetchData();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        ElevatedButton(
          onPressed: _fetchData,
          child: Text("データ取得"),
        ),
        FutureBuilder<String>(
          future: _future,
          builder: (context, snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              return CircularProgressIndicator();
            } else if (snapshot.hasError) {
              return Text('エラー: ${snapshot.error}');
            } else if (snapshot.hasData) {
              return Text('データ: ${snapshot.data}');
            } else {
              return Text("ボタンを押してデータを取得");
            }
          },
        ),
      ],
    );
  }
}
```

## まとめ
- `FutureBuilder` は **非同期処理の結果を元に UI を構築** できる。
- `snapshot` を使って **データの取得状況（成功・エラー・ローディング）** を判定できる。
- `Future<T>` の状態に応じて **`connectionState` を確認** する。
- **ボタン押下などのユーザーアクション** によって `Future` を更新し、UI を変更することも可能。

