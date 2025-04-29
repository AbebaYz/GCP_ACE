### CloudRunの概要
- フルマネージドのサーバレスのコンテナプラットフォーム
- 自動スケーリングで1,000県の同時リクエストを処理可能
- リージョン単位で複数ゾーンにわたり自動複製 (可用性が高い)
- 料金
  - 従量課金
  - 無料枠も存在
  - CPU、メモリ、リクエスト、ネットワーク
- CloudRunはコンテナを配置する
- リクエスト駆動型
  - 処理後は自動的にスケールダウン (ゼロスケール)

**AppEngine(Flexible環境)との違い**
| 項目 | App Engine Standard | App Engine Flexible | Cloud Run |
|------|----------------------|----------------------|-----------|
| コンテナ使用 | 不可（特定ランタイムのみ） | 可能（制限あり） | 完全自由なコンテナ利用 |
| 起動単位 | リクエストベース、インスタンス常駐あり | インスタンス常駐あり | 完全リクエストベース（ゼロスケール可） |
| スケーリング | 自動（一定の制限あり） | 自動（最低インスタンス維持） | 完全自動、ゼロスケール可能 |
| 実行時間制限 | 最長1日（バックグラウンドジョブ制約あり） | 制限なし | デフォルト15分（最大60分） |
| ステートフル性 | ステートレス推奨 | ステートフル可 | ステートレス専用 |
| 起動時間（Cold Start） | 非常に高速 | 遅い傾向あり | 非常に高速 |
| 管理対象 | フルマネージド | VMベースで一部管理必要 | フルマネージド |
| ネットワーク接続 | VPCアクセス可（制限あり） | VPCに統合可能 | VPCアクセス可 |
| 課金モデル | インスタンス起動時間ベース | VM稼働時間ベース | リクエストと実行時間ベース |

---
### CloudRunの作成
- 料金体系
  - デフォルト(requestごとにCPU稼働)
  - 常にCPU稼働
- 複数バージョン作成して、トラフィックを分散させることも可能


---
### コードからのCloudRunのデプロイ
- 既存のコードをデプロイしてみる
1. Dockerコンテナ化
   1. Dockerfileの作成
2. コンテナのビルド (Artifact Registryにpush)
```
gcloud builds submit --tag asia-northeast1-docker.pkg.dev/YOUR_PROJECT_ID/REPO_NAME/my-app
```
3. CloudRunにデプロイ
```bash
gcloud run deploy my-app \
  --image asia-northeast1-docker.pkg.dev/YOUR_PROJECT_ID/REPO_NAME/my-app \
  --platform managed \
  --allow-unauthenticated
```
