# terraform実行環境のセットアップ

## tfenvのセットアップ

### tfenvのインストール
 - brew install tfenv

### パスが通っていない場合、パスを通す
 - brew install tfenv

```bash
$ brew install tfenv
==> Downloading https://github.com/kamatama41/tfenv/archive/v0.6.0.tar.gz
==> Downloading from https://codeload.github.com/Zordrak/tfenv/tar.gz/v0.6.0
######################################################################## 100.0%
🍺  /usr/local/Cellar/tfenv/0.6.0: 19 files, 23.5KB, built in 7 seconds
```

### 任意のバージョンのterraformをinstallする
- tfenv install ${TERRAFORM_VERSION}

```bash
$ tfenv install 0.11.10
[INFO] Installing Terraform v0.11.10
[INFO] Downloading release tarball from https://releases.hashicorp.com/terraform/0.11.10/terraform_0.11.10_darwin_amd64.zip
######################################################################## 100.0%
[INFO] Downloading SHA hash file from https://releases.hashicorp.com/terraform/0.11.10/terraform_0.11.10_SHA256SUMS
tfenv: tfenv-install: [WARN] No keybase install found, skipping GPG signature verification
Archive:  tfenv_download.bj5nlQ/terraform_0.11.10_darwin_amd64.zip
  inflating: /Users/XXX/tfenv/versions/0.11.10/terraform  
[INFO] Installation of terraform v0.11.10 successful
[INFO] Switching to v0.11.10
[INFO] Switching completed
```

### uninstallする時
 - tfenv uninstall ${TERRAFORM_VERSION}
```bash
$ tfenv uninstall 0.11.9
[INFO] Uninstall Terraform v0.11.9
[INFO] Terraform v0.11.9 is successfully uninstalled
```

### 現在インストールしているバージョンを表示
 - tfenv list
```bash
```

### インストール可能なバージョンを取得
 - tfenv list-remote
```bash
$ tfenv list-remote
0.12.0
0.11.10
0.11.9
```

### 指定したバージョンを利用する
 - terraform use ${TERRAFORM_VERSION}
```bash
$ tfenv use 0.11.10
[INFO] Switching to v0.11.10
[INFO] Switching completed
```
