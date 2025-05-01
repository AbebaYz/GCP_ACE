### Bigtableの概要
- 大規模でスケーラブルなアプリケーションをサポートするNoSQLデータベース
- 特徴
  - レイテンシが安定(10ms)未満
  - 高スループット
- ユースケース
  - 高スループットが必要なもの　(アドテックなど)
- BigQueryとの違い
  - Bigtableは高スループット・低レイテンシ`
    - 書き込み・読み込みが頻発するならBigtable
  - BigQueryはSQLベースの集計が得意
    - 分析をメインに行う場合はBigQuery


### cbtによるBigtable操作
- Cloud Bigtable Command Line Tool
- 高コストなため、スループットを必要としない場合は同じNoSQLであるFirebaseなどの検討をするべき

テーブルの作成
```
cbt createtable {table name}
```

テーブル一覧の表示
```
cbt ls
```

列のファミリーを追加
```
cbt createfamily {table name} cf1
```

列ファミリー一覧の表示
```
cbt ls {table name}
```

行r1,列cf1にvalueを入れる
```
cbt set {table name} r1 cf1:c1=test-value
```

テーブルの削除
```
cbt deletetable {tablename}
```
