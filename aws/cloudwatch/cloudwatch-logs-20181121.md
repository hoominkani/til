# awslogs-datetime-formatとawslogs-multiline-patternの使いどこと


## awslogs-datetime-formatの使いどころ
 - awslogs-datetime-formatを使用すると、同一時間帯のログレコードが細分化されず、まとまって表示されるため、可視性が上がる。
 - awslogs-multiline-patternと同時に設定されている場合、このオプションは常に優先される。

```bash
#GMTからの時間オフセットとしての時間帯でログをまとめる場合
"logConfiguration": {
  "logDriver": "awslogs",
  "options": {
    "awslogs-group": "${LOGS_GROUP_NAME}",
    "awslogs-datetime-format": "\\[%d/%b/%Y:%H:%M:%S %z\\]",
    "awslogs-region": "ap-northeast-1",
    "awslogs-stream-prefix": "${PREFIX}"
  }
}
```

## awslogs-multiline-patternの使いどころ
特定のログだけをCloudWatch Logsに送信する際に使う。

```bash
#INFOで始まるログを送信する場合
"logConfiguration": {
  "logDriver": "awslogs",
  "options": {
    "awslogs-group": "${LOGS_GROUP_NAME}",
    "awslogs-datetime-format": "^INFO",
    "awslogs-region": "ap-northeast-1",
    "awslogs-stream-prefix": "${PREFIX}"
  }
}
```

## 注意点
 - すべてのログメッセージに対して正規表現の解析とマッチングを行うため、ログ記録のパフォーマンスが下がる可能性がある。


## 参照
[awslogs ログドライバーを使用する](https://docs.aws.amazon.com/ja_jp/AmazonECS/latest/developerguide/using_awslogs.html)
