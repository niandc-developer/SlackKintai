# SlackKintai
IBM Cloud を使用した Slack 勤怠管理アプリです。

## 環境構築手順

### Node-RED アプリケーションの追加
IBM Cloud ワークスペースで Node-RED Starter ボイラープレートを用いてアプリケーションを作成して下さい。

### Db2 Warehouse サービスの追加
IBM Cloud ワークスペースで Db2 Warehouse サービスを追加し、上で作成したアプリケーションにバインドして下さい。

### Node-REDフローエディタの設定
(1) logic/flow/SlackKintai.json の内容を「読み込み」-「クリップボード」から取り込みます。

(2) 「SlackKintai」タブの dashDB ノードのプロパティを開き、バインドした Db2 Warehouse サービス名を反映させます。「デプロイ」ボタンを押して、全てのエラーが消えるまで繰り返して下さい。

(3) Injectノード「テーブル作成」を実行し、データベーステーブルを作成します。

(4) Web ブラウザで設置したい Slack のワークスペースを開き、SlackApp を作成します。以下の SlackApp 設定を行います。
- Bot User を有効にし、App をワークスペースにインストールします。
- Interactive Components を有効にし、Request URL に https://{Node-REDアプリ名}.mybluemix.net/button-callback を設定します。
```
例）https://slackkintai.mybluemix.net/button-callback
```

(5) Node-REDフローエディタに戻り、「bot_access_token設定」ノードのプロパティを開き、SlackApp の「Bot User OAuth Access Token」の値を設定し、「デプロイ」ボタンを押します。

### SlackKintaiユーザーの設定
(1) 勤怠情報を投稿するチャンネルを作成します。既存の general や random で良ければ作成不要ですが、チャンネル毎に集計表示されますのでグループ毎にチャンネルを作成することをお勧めします。

(2) SlackKintaiを利用したいSlackユーザーはプロフィールの編集で「資格・担当」項目に以下の値を設定します。
```
例1）<KINTAI=general> ※既存 general を使う場合
例2）<KINTAI=random> ※既存 random を使う場合
例3）<KINTAI=kintai>
```
以上までの設定で、朝、夕の所定時間になると、SlackKintai 利用者に通知が飛び、勤怠情報を投入できるようになります。


## Copyright
Copyright 2018 Nippon Information and Communication Corporation

## License
This sample code is licensed under Apache 2.0.

Full license text is available in [LICENSE](LICENSE).
