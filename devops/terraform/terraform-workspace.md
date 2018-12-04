# Terraform workspaceを使う

## ワークスペースの作成、切り替え

```
# dev という名前の workspace を作成して切り替え
terraform workspace new dev
# dev という名前の workspace に切り替え
terraform workspace select dev
```

## ワークスペースの一覧を表示
 - terraform workspace list

```
$ terraform workspace list
  default
* dev
  pro

```

## 環境ごとにtfvarsファイルを分ける

```
# devとproの２つの環境で環境編変数を分ける
$ touch terraform.tfvars.dev
$ touch terraform.tfvars.pro

# ワークスペースdevに切り替え
$ terraform workspace select dev

# ワークスペースdevの変数でterraform planを実行
$ terraform plan -var-file=terraform.tfvars.dev
```

## リソース名を環境ごとに変更

```
tags = {
  Name = "${var.project_name}-${terraform.workspace}"
}
```
