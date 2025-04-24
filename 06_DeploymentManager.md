### Deployment Managerの概要
- GCPの様々なリソースのデプロイを記述する
- IaC (yamlによる構文ファイル)
- template (yamlファイルを生成する方法の一つ、yamlの繰り返しを省略するなど)
  - Jinja
  - Python
- Terraform


### yamlによるデプロイ
```
# 設定ファイル: vm-deployment.yaml
resources:
- name: my-vm-instance
  type: compute.v1.instance
  properties:
    zone: us-central1-a
    machineType: zones/us-central1-a/machineTypes/n1-standard-1
    disks:
    - boot: true
      autoDelete: true
      initializeParams:
        sourceImage: projects/debian-cloud/global/images/family/debian-10
    networkInterfaces:
    - network: global/networks/default
      accessConfigs:
      - name: External NAT
        type: ONE_TO_ONE_NAT
```

gcloudコマンドでデプロイ
```
gcloud deployment-manager deployments create {deploy名} --config {deploymentのyamlファイル}
```

updateするには
```
gcloud deployment-manager deployments update {deploy名} --config {deploymentのyamlファイル}
```

すべてのデプロイを見るには
```
gcloud deployment-manager deployments list
```

デプロイの定義だけを削除した場合は(リソースは残す)
```
gcloud deployment-manager deployments delete {deploy名} --async
```


### Jinjaテンプレートによるデプロイ
- 3つのファイルが必要になる
  - vm-deployment.yaml
  - vm-template.jinja
  - vm-template.py

vm-deployment.yaml
```
imports:
- path: vm-template.jinja
- path: parameter.jinja

resources:
- name: jinja-template
  type: parameter.jinja
```

- jinjaテンプレートではpropertiesにパラメータを渡すことができる
- 一つの型
vm-template.jinja
```
resources:
- name: {{ properties['name'] }}
  type: compute.v1.instance
  properties:
    zone: {{ properties['zone'] }}
    machineType: zones/{{ properties['zone'] }}/machineTypes/n1-standard-1
    disks:
    - boot: true
      autoDelete: true
      initializeParams:
        sourceImage: projects/debian-cloud/global/images/family/debian-10
    networkInterfaces:
    - network: global/networks/default
      accessConfigs:
      - name: External NAT
        type: ONE_TO_ONE_NAT
```

parameter.jinja
```
resources:
- name: jinja-template
  type: vm-template.jinja
  properties:
    name: my-vm-instance
    zone: us-central1-a
```

create
```
gcloud deployment-manager deployments create {deploy名} --config vm-deployment.yaml
```

deleteも同様


### Pythonテンプレートによるデプロイ
- 3つのファイルが必要になる
  - vm-deployment.yaml
  - parameter.py
  - vm-template.py

vm-deployment.yaml
```
imports:
- path: vm-template.py
- path: parameter.py

resources:
- name: python-template
  type: parameter.py
```

vm-template.py
```
def GenerateConfig(context):
    resources = []
    resources.append({
        'name': context.properties['name'],
        'type': 'compute.v1.instance',
        'properties': {
            'zone': context.properties['zone'],
        }
    })
    return {'resources': resources}
```

parameter.py
```
def GenerateConfig(context):
    return {
        'resources': [{
            'name': 'my-vm-instance',
            'type': 'vm-template.py',
            'properties': {
                'zone': 'us-central1-a'
            }
        }]
    }
```

create
```
gcloud deployment-manager deployments create {deploy名} --config vm-deployment.yaml
```
deleteも同様


### Terraformnいよるデプロイ
main.tf
```
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 3.5"
    }
  }
}

resource "google_compute_instance" "vm_instance" {
  name         = "my-vm-instance"
  machine_type = "n1-standard-1"
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-10"
    }
  }

  network_interface {
    network = "default"

    access_config {
      // Ephemeral IP
    }
  }
}
```

```
terraform init  # 初期化
terraform plan  # 変更内容の確認/preview
terraform apply  # 適用
```
