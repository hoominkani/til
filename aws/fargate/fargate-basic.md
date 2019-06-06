# ECS on EC2からFargateへの移行(Terraform ver.)

## はじめに

元々ECS on EC2で管理していたが、EC2の管理から解き放たれるべく、そのままFargateへと移行した。
今回は移行の際にどのような変更が必要であったかを共有する。
なお、インフラリソースの管理はTerraform v0.11.10を使用した。

## 変更対象のリソース

- EC2
 - 管理不要のため削除
 - 踏み台サーバのみ管理
- ECS
 - 詳細な変更内容に関しては下記参照

## ECS 変更箇所

### タスク定義

#### 削除したもの

- mountPoints
  - ホストサーバとマウントをすることはできないので削除

```
- "mountPoints": [
-     {
-         "sourceVolume": "${PATH}",
-         "containerPath": "${CONTAINER_PATH}"
-     }
- ]
```

- volume

```
- volume {
-   name = "nginx.conf"
-   host_path = "/nginx.conf"
- }
```

- portMappings
  - ホストポートのマッピング指定はできないので削除

```
- "hostPort": 80
```

- link
  - link設定はできないので削除

```
- "links": [
-     "app:app"
- ]
```

#### 追加したもの

- requires_compatibilities
- network_mode

```
resource "aws_ecs_task_definition" "app" {
  requires_compatibilities = ["FARGATE"]
  network_mode             = "awsvpc"
}
```

#### 変更したもの

- cpu
- memory

ECS on EC2では自由に設定できていたが、Fargateではあらかじめ定められたパラメータの中から選択することになる。

※ 2018/12/06 現在時点でのパラメータ

| CPU   | メモリ ※1GB=1024  |
|---|---|
| 256 | 512 / 1024 / 2048 |
| 512 | 1024 / 2048 / 3072 / 4096 |
| 1024 | 2048 / 3072 / 4096 / 5120 / 6144 / 7168 / 8192
| 2048 | 4096 ～ 16384 ※1024ずつの加算 |
| 4096| 8192 ～ 30720 ※1024ずつの加算 |

### ECS Service変更箇所

####追加したもの

launch_type = "FARGATE"

network_configuration {
+    subnets = [
+      "${aws_subnet.fastladder_public_a.id}",
+      "${aws_subnet.fastladder_public_c.id}",
+    ]
+
+    security_groups = [
+      "${aws_security_group.fastladder_alb.id}",
+      "${aws_security_group.fastladder_web.id}",
+    ]
+
+    assign_public_ip = "ENABLED"
+  }

iam_role
execution_role_arn       = "arn:aws:iam::${var.aws_id}:role/ecsAdminRole"

## ターゲットグループ変更箇所

#### 追加したもの

- target_type

Fargateの場合、ターゲットグループのtarget_typeにはipを設定する必要がある。

```
target_type = "ip"
```

## 終わりに

今回は必要最低限の変更内容に関してまとめました。
(EC2のuserdataで実行させていたコマンドを別に移動など、プロジェクトによって)
