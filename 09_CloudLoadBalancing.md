### Cloud Load Balancingの概要
- GCPの負荷分散サービス
- トラフィックの分散を担当する
- 特徴
  - レイヤー
    - HTTP(S)負荷分散 (layer 7: application層)
    - ネットワーク負荷分散は (layer 4: transport層)
  - 負荷分散箇所
    - グローバル
    - 内部
  - リージョン
    - 負荷分散の対象となるVMインスタンスは、同じリージョンにある必要がある
- Cloud Loggingなどの機能もある
- Managedサービス


| 種類 | プロトコル | グローバル or リージョン | 主な用途 | なぜその用途になるか |
|:---|:---|:---|:---|:---|
| **HTTP(S) Load Balancer** | HTTP, HTTPS | グローバル | Webアプリ、APIなど | L7レベルでリクエスト内容（パスやヘッダー）を見て振り分けでき、世界中のユーザーに最適な経路を自動選択できるため。 |
| **TCP Proxy Load Balancer** | TCP | グローバル | TCPアプリ（例：メールサーバ） | L4レベルでTCPコネクションを最適なリージョンへ中継できるため、大規模TCPサービス（SMTPなど）に向いている。 |
| **SSL Proxy Load Balancer** | SSL/TLS | グローバル | 暗号化通信アプリ | クライアントとのSSL/TLS通信をLBで終端して、内部は復号通信できるため。大量のSSLセッションを高速にさばく必要がある場合に適している。 |
| **Network Load Balancer (外部)** | TCP/UDP | リージョン | ゲーム、VoIP | L4レベルで極めて低レイテンシかつ大量のTCP/UDPトラフィックを捌けるため。特にUDPを使うリアルタイム通信（ゲーム、通話）に向く。 |
| **Internal Load Balancer** | TCP/UDP | リージョン | 内部マイクロサービス通信 | GCP VPC内部だけで通信するため、外部にIPを公開せず、低レイテンシ・高セキュリティなシステム間通信に適している。 |
| **Internal HTTP(S) Load Balancer** | HTTP/HTTPS | リージョン | 内部Web API通信 | 内部向けにHTTP/HTTPSトラフィックのパスベースルーティングを行いたい場合に使用する。マイクロサービスや社内API連携向き。 |
