### KubernetesEngineの概要
- コンテナのオーケストレータ
  - たくさんのアプリケーション(Docker Container)を管理するシステム
- Kuberenetes
  - open sourceのコンテナオーケストレーションプラットフォーム
  - 要は「たくさんのコンテナをうまくまとめて動かすための管理システム」
  - 役割
    - デプロイ管理：アプリを自動で起動・更新・復旧
    - スケーリング：負荷に応じて自動でコンテナの数を変更
    - ロードバランシング：リクエストを複数のコンテナに振り分け
- モード
  - Standard : 手動管理
  - Autopilot：自動でpod/nodeの管理
- Anthos
  - マルチクラウドのK8s
  - GKEとEKS（AWSのK8s), AKS(AzureのK8s)と連携する
- K8s用語
  - Pod
    - コンテナの最小実行単位
    - 1つまたは複数のコンテナを格納した「箱」
    - 同じpod内のコンテナは同じIPアドレスとストレージを共有する
  - Deployment
    - Podをどの用に配置するか？
    - Podの自動復元・スケーリング
  - Service
    - Podにどのようにトラフィックを流すか？
    - Podは壊れるたびに再作成され、IPが変わりやすいので、固定の入口を作成する
- 設定方法
  - GCPコンソール
  - Kubectl : yamlファイルによる作成

---
### GKEのアーキテクチャ
- Master Node
  - 全体をコントローするためのもの
  - Kubectlを使用して管理
- Node
  - Compute Engine
  - Podを実際に動かすマシン
  - 中身
    - kubelet : Node上でPodが正しく動いているか監視する
    - kube-proxy : ネットワーク通信の中継
    - コンテナランタイム : 実際にコンテナを動かす
- Cluster
  - 複数のNodeからなるグループ
  - ClusterはどのNodeにどのPodを動かすかを決定する

---
###　コンソールによるGKE作成
- 負荷分散
  - Service : Layer4
  - Ingress : Layer7
- GKE Standard
  - Node単位の課金
- GKE Autopilot
  - Pod単位の課金

---
### yamlファイルによるGKE作成
```
kubectl apply -f {yamlファイル}
```
