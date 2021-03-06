# クラウドGPUインスタンスの料金比較

## AWS、Google、Azureなど、各社の価格

機械学習には欠かせないGPUインスタンス。
各クラウドサービスではどのようなコスト感になっているのか、比較してみました。

### 前提条件

- リージョンは東京もしくは東アジアです。
- 2018年11月30日現在の価格です。
- Linuxの価格です。
- RAM、ストレージの単位はGBです。

### AWS

#### オンデマンドインスタンスとスポットインスタンス

| インスタンスタイプ | GPU | GPU メモリ| vCPU | メモリ | 時間単位の金額 <br> (オンデマンド) |　時間単位の金額 <br> (スポット) |
|---|---|---|---|---|---|
| p3インスタンス　 | 1 ~ 8 | 16 ~ 128 |  4 ~ 64  | 61 ~ 488 | $5.243 ~ $41.944 | $1.5729 ~ $41.944 |
| p2インスタンス | 1 ~ 16  | 12 ~ 192 |  8 ~ 64  | 61 ~ 786 | $1.542 ~ $24.672 | $0.4626 ~ $24.672 |

<br>
#### Amazon EC2 Elastic GPU

| Elastic GPU サイズ | GPU メモリ | 時間単位の金額  |
|---|---|---|
| eg1.medium ~ eg1.2xlarge | 1 ~ 8 | $0.093 ~ $0.744 |

<br>
### Azure
#### 従量課金

| シリーズ   | GPU | vCPU | RAM | 一時ストレージ | 時間単位の金額  |
|---|---|---|---|---|
| NV シリーズ | 1 ~ 4 | 6 ~ 24  | 56 ~ 224 | 340 ~ 1,440 | ¥176.96 ~ ¥707.84 |

<br>
### GCP
#### プリエンプティブインスタンスとノンプリエンティブインスタンス

| GPU モデル | GPU | GPUメモリ | 利用可能なvCPU 数 | 利用可能なメモリ | 時間単位の金額 | 時間単位の金額(プリミティブ) |
|---|---|---|---|---|---|---|
| NVIDIA® Tesla® V100 | 1 ~ 8 | 16 ~ 128 | 12 ~ 96 | 78 ~ 624 | $2.48 ~ $19.84 | $0.74 ~ $5.92 |
| NVIDIA® Tesla® P100 | 1 ~ 4 | 16 ~ 64 | 16 ~ 96 | 104 ~ 624 | $1.60 ~ $6.40 | $0.43 ~ $1.72 |
| NVIDIA® Tesla® P100　<br> 仮想ワークステーション | 1 ~ 4 | 16 ~ 64 | 64 ~ 96 | 208 ~ 624 | $0.49 ~ $1.96 | $0.135 ~ $0.54 |

<br>
### さくらインターネット
#### 従量課金

| モデル   | GPU | GPU搭載メモリ | 時間単位の金額  |
|---|---|---|---|
| Tesla P40 | 1 | 24 | ¥349 |
| Tesla P100 | 1 | 16 | ¥357 |

<br>
## スペックの近いインスタンスの料金を比べてみた
### 条件

- オンデマンドの料金である
- 日本円換算の箇所は、1ドル113.39円の計算である(2018/11/30 現在)

### 比較結果

| サービス名 | シリーズ名／モデル | GPU | 時間単位の金額 |
|---|---|---|---|
| AWS | p2インスタンス | 1 | $1.542 (約 ¥174.84) |
| GCP | NVIDIA® Tesla® P100 | 1 | $1.60 (約 ¥181.41) |
| Azure | NV シリーズ | 1 | ¥176.96 |
| さくらインターネット | Tesla P100 | 1 | ¥357 |

<br>
現在のところ、さくらインターネット以外の各社はほぼ似た価格帯となっていますね。
あとは各社が出している機械学習む恵顗のサービスやMLaaSなどを比較してみるのもいいでしょう。
