### gcloudコマンドの概要
gcloudリソースの作成と管理を行うツール
gcloudはcloudsdkの一部
cloudshellではセットアップされてる


### gcloudコマンド主要なもの
コンフィグの切り替え(projectごと)
```
gcloud config
```

全てのコンフィグをリストアップ
```
gcloud config configurations list
```

現在のコンフィグの中身を確認する
```
gcloud config list
```

新規コンフィグを作成
```
gcloud config configurations create {コンフィグ名}
```

このままでは認証してないのでログインする
```
gcloud auth login
```

vm作成
```
gcloud compute instance create
```

projectの作成
```
gcloud projects create {プロジェクト名}
```

projectとconfignの紐づけ
```
gcloud config set core/projects {プロジェクト名}
```

VM一覧のリスト
```
gcloud compute instances list
```

IAMポリシーの確認
```
gcloud projects get-iam-policy {プロジェクト名}
```

configの切り替え
```
gcloud config configurations activate {コンフィグ名}
```

configの削除(shut down)
```
gcloud config configurations delete {コンフィグ名}
```
