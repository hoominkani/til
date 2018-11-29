#Javascript で機械学習はじめよう
 - Shuhei Iitsuka

## tensorflowを使ってこれまで作ったもの
 - Emoji Scavenger Hunt
  - お題として出てくる絵文字を現実世界で見つける(カメラで認識)

 - Gboard物理手書き入力
  - キーボードの上で文字を手入力できる機能

## 機械学習の定義
 - データを活用して有用な予測を行うこと
 - 人間やがるプログラミングとは違い、モデルがロジックを考える
 - ロジックを記述することが難しいとき、データからロジックを生成する

## 機械学習の実践方法
 - １）k近傍法
  - もっとも距離の近いk個のデータ点で多数決を取るアルゴリズム
  - データが増えると計算が増える
 - ２）線形モデル
  - 二つのグループを分ける平面を見つけて、分類に利用する
  - 平面で分けられる問題ばかりではない
- ３）ニューラルネットワーク
 - ネットワークの構成次第では、平面以外の分離面も描ける

## Deep Learning
 - ニューラルネットワークを重ねたもの
 - パラメータ調整が多い

## TensorFlow
 - データフローグラフを使用して数値計算を行うためのOSS

### 具体的には何をしているのか
 - ニューラルネットワークの計算式を計算グラフとして表現できる
 - 計算グラフを用いることで、微分計算の実装が容易になる
 - 誤差逆伝播法：誤差から徐々に計算してパラメータの偏微分を求めて修正するテクニック

## TensorFlow.js
 - TensorFlowのJavascript ver
 - オンブラウザ機械学習が可能
  - 高速な推論が可能
  - プライバシーの保護
  - スケーリングが容易
  - 学習済みモデルの軽量化が課題

## 五目並べを作ってみる
 ### ○×判別機を作る
  - 何を○として、何を×とするか

Node.js: The Road to Workers
- Anna Henningsen

The golden rule of Node.js performance: Don't block the event loop

# Diagnose your Node.js app
 - Daiki Arai

## 初学者の悩み
 - 非同期処理が難しい
  - APIの実行順が直感と違うなど
 - エラーハンドリングが難しい
  - 選択肢が多い
 - debugが難しい
  - スタックトレースが途切れる場合があるなど

## 非同期処理が難しい
 - ブラウザで実行した場合、10系、11系それぞれで実行順が異なる場合がある
 - 非同期APIは互換性は非保証
 - 非同期関数と同期関数が混在したコードだとバグのような挙動があっても再現性がない場合がある
 - フロー制御を実行順に依存しない設計にする必要がある
  - 非同期I/Oの実行順は不規則
  - 確認方法
    - Async Hooksで実行順を見ることができる
    - 非同期I/O、タイマー、Promiseなどトレースできる
    - tips: typeが分かりにくい場合は、スタックトレースで行番号を取得

## エラーハンドリングが難しい
 - Callback型はPromise化できる
 - (EventEmitterを除けば)Promiseでのハンドリングで統一可能
 - Promiseに統一すれば安全？
  - 潜在的にmemory leakなどが起きる可能性
  - unhandledRejection
    - expressならエンドポイントごとにcatch漏れを防ぐwrap関数を挟むことを推奨
    - 発生時にcrashさせるべきかコミッター間でも議論になっている
  - mutipeResolves
    - 複数回resolve/rejectが呼ばれたばあいに発火

## debugが難しい
 - 12系からasyncスタックトレースが強化される可能性あり
  - 非同期継承が開始されると、それまでスタックトレースでは継承されなかったが、継承されるようになる
  - これによって呼び出し元も出るように
 - 本番アプリがcrashした場合
  - post-mortem debugging
    - クラッシュ時のプロセスのメモリイメージから市長を得る方法
    - 通常のスタツクトレースよりも多くの情報を取得できる
    - クラッシュしたプロセスを再起動させつつdebugを並行して行える
    - 流れと準備
      - Core Dump設定
      - Process Crash
      - Process Restart
      - core dumpの解析

# State of SEO for SPA
 - seya

## SPAはSEOに弱い？
 - ネット上には様々な情報が錯綜
 - 今回はSEOの土台作りに関してまとめる(Google向け)

## SEOとは？
 - 検索エンジンでより上位に表示されるための施策
   - Goole Botにクロールされること
   - htmlが適切に解釈されること
   - OGPやTwitter Card
   - 構造家データ
    - 例: AMP
    - 動画

 ## Goole Botについて
  ###　課題
    - JSを実行しない？　→　実行する
      - レンダリングエンジンはchrome41相当の機能しか持っていない
        - そのため、アロー関数などは使えない
      - wensocketプロトコルを対応していない
      - ユーザのどう家お必要とする機能は自動で不承認になる
    - Ajaxを実行してくれない/待ってくれない　→　実行される
      - レスポンスに時間がかかりすぎるとインデックスされない
      - 何秒なら待ってくれるのか？
        - Fetch ad Googleだと約５秒
        - NaturalなGoogle botは約20秒
      - ジョン・ミュラー氏のメールだと決まった時間は定めていないが、５秒は良い線いっているとのこと。
    - メタ情報はサーバから返す時点でHTMLに含まれる必要がある
    - Render Queueによるインデックスの遅延
     - 通常の静的なサイトとは違い、Render Queueに移譲される →　１週間かかることも
### Googleの方針
 - Google dev summitでの発表
  - chrome41相当のレンダリングエンジンとRender Queue問題に関しては将来的に解決されそう

### 解決策
 - chrome41でレンダリングできるようにする
   - Fetch as Googleで自分のサイトに対してリクエストを行う
    - しかし、１日１０回までしかできない
    - 一時的にアクセスできませんの原因不明のエラーが出たり、不安定なことも
  - pupeteerでエミュレートできる
    - polyfillをかけるのでファイルサイズは膨らむ
- メタ情報だけSSR
  - Nuxt.js mode SPAではメタ情報もサーバで返してくれる
- Dynamic Rendering
 - アクセスがGoogle Botかどうかを判断し、キャッシュされたメタ情報を返す
  - クローキング
    - ブラックハットSEO
    - botとユーザーに別のコンテンツを返す。
    - 見つかるとペナルティが課せられる
    - Google自体がDynamic Renderingを推しているので、クローキングには当たらないと考えられる
- Static Site Generator
- SSR
 - サーバー側でJSを実行してHTMLを返す
 - 注意点：SSRでもタイムアウトは有り得る
 - 実行しているJSが重く、パフォーマンス対応されていない場合、インデックスされないことも

### 対策の指針
 - インデックスに信頼性を求めるか
 - メタ情報の対応が必要/不要
 - 頻繁に更新される&すぐに反映したいか否か　

### SSRが必要かどうか
 - SEO観点では不要
 - Dynamic Renderingより高コスト

# Node.jsアプリの開発をモダン化するために取り組んできたこと
- Daiki Yokoi

## ソースコード編

### Background
- 既存のアプリはNode.js+Expressの構成
- フロント側にAngular.jsの知見があった

### 試したツール
- InversifyJS: IoCコンテナ
- routing-controller
- tsoa: APIドキュメントの自動生成

### 結果
- 繋ぎ合わせるのが面倒、統合された物が欲しくなった
- Nest
 - 欲しかった機能が一通り整っていた
 - ポピュラーになりそう、勢いがあった
### そもそもNestとは
- 簡単に言うとクラスの集まり
- 複数もモジュールがツリー状になってアプリを構成
- コントローラーではデコレータでハンドラを登録する
- プロバイダは各種ビジネスロジックを担当
- 依存関係はコンストラクタの実装を元に解決される

### recipe
- APIドキュメントを自動で作成し、SwaggerUIに登録
- ロギングやレスポンスの整形に便利なインターセプタ
- クエリパラメータと同時に定義するバリデーション
 - クライアントサイドにエラーを返す時のコントロールがしづらい
- ガードによってアクセスコントコールを実現
 - ガードは不正なリクエストを弾くための仕組み
- TypeORMでのデータベースアクセスをサポート
 - TypeORMはポピュラーなOR Mapper

### その他
- nestjs/testingパッケージ
- コントローラー部分はREST以外にも対応

## ユニットテスト環境編

###　Background
- ローカルにインストールしたMySQLやRedisを利用
- AWSの認証情報をローカルで利用
 - 使っていないと思っていたが、実は使っていた例など有り

### Solution
- MySQL,Redis
- LocalStack
- ユニットテストでのDockerの利用
 - docker compose
   - 初心者でも扱いやすい
 - CI連携：コンテナとの親和性が高い
- テストツール
 - Jest
   - Facebook製
   - マルチプロセスで高速
   - チェック用関数がプリインストールされている
 - MockDate：データをモック化

## インフラ編

### サーバーレス環境の探求
- Elastic BeanstalkからFargateへの移行
 - Elastic Beanstalk
   - 高速でイミュータブルなデプロイ
   - その一方、EC2の管理コストが高い
 - Fargate
  - フルマネージド、スケーラブル
  - Fargateのスケーリング
   - ECS task
   - ECS Service
 - Elastic Beanstalkからエンドポイント単位で移行中
### Infrastructure as Code
- CloudFormation Designerを使ってみるのオススメ

# WebアプリをNativeアプリにする Capacitor が広げるWebの可能性
- 榊原 昌彦

## Capacitorとは
- HTML5をiOS,Android,Electronで配信するためのプラットフォーム
- 次世代のCordova

## HTML5アプリ
- アプリというWebviewを使ってHTMLを表示
- デザインガイドラインに沿って作るのでアプリのように見える
- Ionicフレームワークなどのモバイルフレームワークが使われる
- SPAで作ることができる
- ReactNative/NativeScriptとの違い
 - ReactNative/NativeScriptはJavascriptCoreを通すことでコンパイルしている

## Apache CORDOVA
- 無料
- 課題
 - バージョン問題
   - バージョンの組み合わせでビルドに失敗しやすい
 - プラグイン問題
   - 保守されていないプラグインもよくある
 - デザイン
   - iOSなどのデザインが変わった場合、それに追従するためのコストがかかる
 - 開発デザイン
   - OSSなのでプルリクがマージされるまでが長いこともある

## Capacitor
- 画面表示+ネイティブAPIのようなアプリに良い
- Cordovaに比べ、簡単にNative連携が可能
- Native UI Shell
 - NativeとWeb Viewの融合
- PWA Elements
- npm依存(二重管理からの脱出)
- Cordovaプラグインサポート
- Nativeに比べて遅くないかとよく聞かれる
 - 速くもないが、遅くもない
 - Facebookくらいのアプリであればそこまで速度が変わらない
 - 遅い場合、以下のような実装ミスが多い
  - tapableをつけずにdivにクリックイベントをつける
  - AngularでJITコンパイル
  - 実機ではなくエミュレータで動作確認(実機だと変わらないことがある)

## Progressive Web Apps
### アプリを利用するコストの高さ
- モバイルの利用時間は増加傾向
- スマホアプリの新規インストールは2/3は0(一ヶ月)
- かつスマホアプリはTOP5が独占
- スマホアプリに比べ、WEBは倍のトラフィック
- 色んなWEBに訪問される
- つまり、今後はWEBでアプリケーションを利用した人の中のコアユーザーがスマホアプリを使っていく時代へ

# 実践GraphQL for クライアント側
 - 鈴木 亮太

## GraphQLって何？
 - 型システムとともにあるquery language
 - 最近foundationができた
 - API用のクエリ言語
 - データフェッチにフォーカスした仕様

## Query/Mutation
 - GraphQLのエンドポイントに対する????
 - フィールドに引数を渡すことが可能
 - データの関連を辿ってデータが取れる
 - 型システム
  - String, Int, Floatなどベーシックな型 + ObjectType

## GraphQLを使ったプロダクト紹介
 - Growlio??
   - 広告配信システムの管理画面
   - やたらデータ同士が関連を持つ
   - backend: scala, frontend: elm
 - なぜ使おうと思ったか？
  - 別のプロダクトで同じようなアプリを作った(Restful)苦しみから
  - サーバ,クライアント感のイケてなさ
    - API仕様のやり取りはマークダウンのテーブル
    - コミュニケーションはGraphQLのスキーマ中心に
    - ドキュメントはコードから生成　→　人的ミスがなくなる
  - エンドポイントがたくさん
    - 一つの画面を表示するために多くのエンドポイントとやり取りが必要
    - GraphQLだとレスポンスは返って来れば信用できる
  　- introspection: 型システムのメタデータを取れる仕組み
  - データ取得のパフォーマンスのボトルネック化
    - エンドポイントの数だけネットワークの行き来がかさむ
      - GraphQLになるとリクエスト一回で済む
    - 必要のないフィールドも送られてくる
     - GraphQLだと必要なフィールドのみが送られてくる

## GraphQLを使ってみて
### 困ったこと
 - リクエストが/graphqlになることで、レスポンスタイムを見てのボトルネック探しができなくなる

### 良かったこと
 - 困ったこともあるが、クライアントサイドからすると旨味しかない

### 工夫
 - Query/Mutationには名前をつける
  - ログからクエリ送信の文脈が分かる
 - fragmentを積極的に使う
  - クエリの再利用性を高める
  - ライブラリ越しにGraphQLクエリを生成していると忘れがち

# Service Workerを用いたキャッシング戦略 〜Wikiアプリケーションを例に〜
- 飯塚 大貴

## Service Workerとは
 - オフラインで動作させるため、ブラウザがWebページとは別にバックグラウンドで実行するスクリプト
 - DOMにはアクセスできない

## Service Worker
 - 導入前
  - 何をキャッシュするかブラウザ任せ
 - 導入後
  - 開発者によってキャッシュからとるもの、ネットワークからとるものを選択可能に

## キャッシュパターン
 - キャッシュファースト
 - ネットワークファースト

## Scrap Box
 - 基本SPA
 - ページコンテンツ
  - 都度APIを呼んでJSONを取得
 - 最初のHTMLもcacheから返す
 - 生成から1ヶ月以上前のものはネットワークに取りに行く
 - アセットもキャッシュファースト
  - 画面表示のためのアセットをDLできたら、更新があるものをDL
  - ServiceWorkerに頼らず、アプリ画面表示のたびにキャッシュが最新であるか確認
  - キャッシュすべきアセットはリスト化
 - サイレント自動アップデートを実施
  - ユーザーが気づかないところでbackgroundで更新を行う
 - tips: chromeのプライベートモードはlocalcache割り当てが小さいため、キャッシュ容量超過のデバッグに便利

## prefetch
## prefetchするかどうか
  - 低速ネットワークではprefetchしたくない
  - ネットワークの接続状況に応じてprefetchするかしないかを切り替え

## prefetchして良かったこと
 - 動作が高速
 - レイテンシの大きい環境でしか出ないバグが表面化した

## tips
 - navigater.onlineを信用しない
  - wi-fiに繋がっていても認証していない可能性があるので、実際にリクエストを投げてみてレスポンスが返ってくるかどうかを確認すべき
 - cache名に日付を使う
  - 字面を見るだけで消すべきキャッシュかどうか分かる

## これからやりたいこと
 - cachestrageを使う
 - IndexedDMも使う
  - pageごとに取得、更新できる
 - ServiceWorkerのBackground Syncを使う
  - まだchromeのみでしか使えない

# 貢献できるOSSの見つけ方 -完結編-
 - Masato Ohba

## 課題：contributionに参加したいけどできない
 - 課題の見つけ方２種類
   - プロジェクトを選ぶ
   - 偶然発見
 - 好きなプロジェクトをウォッチする
  - モチベーションは上がるが、ハードルが高くなりがち
  - 小さな成功体験を重ねた方がモチベーションが長続きする
 - contributionの理想形
  - contributionをしたい人が課題を見つけやすくなる
  - goofi
    - メンテナー・コミッターがcontributionを求めているIssueをまとめたサイト
    - netlify →　heroku　→　Github API
    - v2: PerformanceとRate limitに課題あり
    - v3: Now.sh(SSR with Next.js + GraphQL)
    - tips: Now.shは無料枠でもスリープしない設定にできる
## OSS活動を通して面白かったこと
 - お金をもらえた
 - Issueはあるが答えがないこともある

# Vue.js/Nuxt.js で 実現できた PWA の リアルタイム動画ラップ・バトル・アプリ
- lulzneko

## ハッカソンで作成したアプリ
 - タップ、タップ、アップ
  - Vue.js,Nuxt.jsで実装
   - Nuxt.jsは環境構築が楽
  - アーキテクチャ
   - 動画配信: SkyWay
    - community Editionなら無料で利用可能
    - SDKが用意されており組み込みが楽(しかしSafariへの対応がなかった)
   - Infra: API Gateway + Lambda + DynamoDB + Firebase(Feedback&chat)
  - Typescript
   - Lambdaのコールドスタートに強い
  - Serverless Framework
   - AWSの環境構築とデプロイが楽