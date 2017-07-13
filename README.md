# express-session sample on Bluemix

このコードに関する解説は、Qiita [Node.js Express4で Cloudant セッション・ストアの水平分散クラスタを構成する](http://qiita.com/MahoTakara/items/507dacf5a5dc81705d50) にありますので、合わせて参照してください。

# 実行するために必要事項

* [Bluemix アカウント](https://console.bluemix.net/)
* [Bluemix CLI のインストール](https://clis.ng.bluemix.net/ui/home.html)
* [Bluemix Cloudant Liteプランの作成](https://console.bluemix.net/catalog/services/cloudant-nosql-db?env_id=ibm:yp:au-syd)
* [git コマンドのインストール](https://github.com/)


# ローカル環境で実行する場合

(1) Bluemix で Cloudant Lite プランを作成します。
(2) vcap-local.jsonファイルを編集して、Cloudantのサービス資格情報をセットします。
(3) 必要なモジュールをインストール

~~~
npm install
~~~

(4) セッション・ストア用のデータベースを作成します。

~~~
node ./create_db.js
~~~

(5) アプリをスタートします。

~~~
npm start 
~~~


# Bluemix で動作させる場合

(1) Bluemix で Cloudant Lite プランを作成します。
(2) manifest.yml を編集します。 編集箇所は以下の２箇所です。

~~~
applications:
- path: .
  memory: 128M
  instances: 2
  domain: mybluemix.net
  name: express-session-test
  host: express-session-test-tkr  <---　重複ない様にする
  disk_quota: 1024M
services:
- Cloudant NoSQL DB-zj  <--- 自分のインスタンス名に変更する
~~~

(3) bx cf push で、Bluemix 上にデプロイする

~~~
$ bx cf push
~~~


