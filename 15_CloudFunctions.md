### CloudFunctionsの概要
- サーバーレスでスケーラブルな従量課金制の関数 (FaaS)
- 負荷に応じた自動スケーリング
- 最小権限の原則に基づいた、ロールごとのセキュリティ
- 非常に安いのが特徴
  - 200万回までの呼び出しは無料
- ユースケース
  - GitHubにpushした場合に、それを検知してslackに通知する
  - 処理が重いようなものをアプリサーバ上での処理ではなく、CloudFunctionsに委譲する
- マイクロサービスの1 partとして有効活用可能
  - 単一の関数のみ
- 「あるイベントが発生したらすぐにちょっとした処理を行う」というユースケース

---
### CloudFunctionsnの作成
- トリガーに様々なイベントを設定することができる
  - HTTPSによるアクセス
  - Pub/Subなど
