### Datastoreの概要
- NoSQLのデータベース
- Webアプリやモバイルアプリなどのためのスケーラビリティが高いDB
  - 世界中にインスタンスを作成してスケーリングすることができる
- 強整合性と結果整合性の両方に対応
  - 結果整合性
    - データを書いてから反映されるまで時間がかかる
  - 強整合性
    - データを書いたら必ず読み出しに反映される
- データベースモードを必ず指定する必要がある　(将来的にはすべてFirebaseになる)
  - Firebase
  - Datastore
- データ構造
  - 名前空間
    - スキーマみたいなもの
  - 種類(kind)
    - テーブルのようなもの
  - entity
    - 列のようなもの
  - property, key
    - カラムむと値のようなもの
- entity間には祖先関係をつくることができる

- 抽出にはGQLという言語を使用する
  - SELECT * FROM {kind名}


---
### Firestoreの概要
- Global アプリ用に構築されたNoSQLデータベース
  - モバイルアプリやウェブアプリのデータ保存や動機、照会がグローバルスケールで利用可能
- Datastoreの後継
- サーバーレス
- Data構造
  - Collection
    - documentのコンテナ
  - Document
    - データストレージの基本単位
  - データ
    - 具体的なデータ
  - 階層データ
    - コレクションの中にコレクションを作成
