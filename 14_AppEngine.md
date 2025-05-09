### AppEngineの概要
- フルマネージド型の**サーバーレス**なアプリケーション (**PaaS**)
- IaaS
  - Compute Engine
  - ハイパーバイザーなどの物理実態までをGoogleが管理
  - ゲストOSやapp実行環境などはユーザが定義
- PaaS
  - app実行環境までgoogle が管理
  - ライブラリやappコードなどをユーザが管理
  - ライブラリ開発などの部分に注力することができる
- サーバレスでコードを追加するだけ
  - Node.js, Java, Ruby, C##, Python,...
  - 独自ランタイムも利用可能 (Dockerなど)
- 従量課金性
- 機能 (IaaSで行う手間を削減)
  - 自動スケール
  - ユーザ認証
  - バージョン管理
  - トラフィック分割
  - 実行スケジューリング
- 環境
  - 標準環境 (Standard)
    - googleが用意したランタイム環境で高速起動、小規模アプリ向け
  - Flexible
    - Dockerコンテナのような環境構築をすることができる

---
### スタンダード環境とフレキシブル環境
- Standard環境
  - サンドボックス内で特定の言語ランタイムで作動する
  - 迅速なスケーリングに対応する必要のあるアプリ
  - 特に動かなければ0インスタンス(無料)で動く
  - インスタンスの起動時間 (sec)
  - ランタイムの変更は基本できない
  - 料金はインスタンス時間に基づく
- Flexible環境
  - Dockerのような環境
  - 一定したトラフィックを受信するアプリ
  - インスタンスの起動時間 (分)
  - VMの使用料に基づく
  - 最小使用料金は分単位

---
### スタンダード環境のデプロイ
- [参考repository](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/main/appengine)
- AppEngineでpythonアプリケーションを動かすためには、yamlファイルで設定をする必要がある

アプリディレクトリ直下で以下のコードを叩く必要がある
```
gcloud app deploy
```

- AppEngineが自動でインスタンスに振り分けるのでポートなどを考える必要はない
- AppEngineはデプロイするたびにバージョニングすることができる
  - さらにトラフィックをバージョンごとに分割することができる
  - A/Bテストやカナリアデプロイ等に使用可能

---
### フレキシブル環境のデプロイ
- application開発の流れ
  1. ローカルで開発とテスト
  2. deploy command `gcloud app deploy`
  3. GCPでの動作確認
  4. 本番環境での使用
- `app.yaml`で`env:flex`という設定をしなければならない
- Dockerコンテナにはlayerがある
  - ベースレイヤ→ミドルウェアレイヤ→アプリケーションレイヤ→...
  -
