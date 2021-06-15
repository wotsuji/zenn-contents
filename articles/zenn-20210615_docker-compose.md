---
title: "docker-compose.ymlの書き方を整理する"
emoji: "😺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["docker","dockercompose","linux","wsl2"]
published: true
---
# はじめに
dockerは便利です。WSL2のUbuntuでも普通に使えます。一時的な環境を作成したりする事も容易です。ただし docker-compose.yml の書き方に慣れが必要と思いますので整理しておきたいと思います。 
※前提としてdockerとdocker-comooseはセットアップ済、dockerfileではなくdocker-composeを利用する事を想定しています。

> WSL2の場合はDocker for Windowsを使ってDocker環境を作る記事をよく見かけます。Docker for Windowsを利用するとvs_codeなど統合開発環境と連携できるなどメリットもあると思うのですが、まずはLinux版でのインストールでコマンドからの使い方に慣れる事を推奨したいです。

# サンプル
```
version: "3.8"

services:
  db:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: mysql_root_paswsword
      MYSQL_PORT: 3306
    ports:
      - 3306:3306
    volumes:
      - ./mysql-data:/var/lib/mysql
  web:
    image: httpd:latest
    restart: always
    volumes:
      - ./webapp:/webapp
    ports:
      - "8080:80"
    depends_on:
      - db
```
データベースはmariadbを利用して3306ポート、mysql-dataをマウントしてデータベースを永続化しています。WEBサーバはApacheの80ポートに対して8080ポートを割り当ててます。これだけ知っておけば環境の起動までは最低限で出来るというサンプルです。

# 設定項目の確認
設定項目を順に確認したいと思います。設定はインデントで階層を作って入れ子にして記述していきます。volumes や ports など外部との接続系の記述は「左（ローカル）：右（コンテナ）」という関係になります。

- **version（第一階層）**
「docker-compose.yml」の記述方法はバージョン依存があるため、どのバージョンで記述したのかを宣言します。2021年6月11日時点の最新は 3.8 です。
※ どの辺りが変わるのかというと公式の案内を見ないと解らないですが、バージョン2と3では違いが多いそうです。

- **services（第一階層）**
ここからサービスを記述します。という宣言です。

- **db（第二階層）**
サービス名称 サービス名「db」はユーザーが自由に付ける事ができます。ネットワークで接続する際の別名にも使われます。

- **image（第三階層）**
「docker hub」のイメージを利用する場合にイメージ名を指定します。

- **restart（第三階層）**
no ： コンテナを再起動しない(デフォルト）
always ： コンテナが停止すると常に再起動する。
※ dockerは起動と停止を繰り返すので今回はalwaysを指定しています。

- **environment（第三階層）**
コンテナに設定する環境変数です。docker hub のイメージによって設定できる環境変数が違うため、直接 docker hub を見に行くのが良いと思います。
※ それぞれに設定用の環境変数がある前提ですが、DBのユーザーとサービスのDB接続ユーザーをそれぞれ設定しておく。という使い方が便利と思います。

- **ports（第三階層）**
外部とポートのフォワードで接続ができます。
localhost:8080 に接続すると コンテナ：80 にフォワードする設定になります。

- **volumes（第三階層）**
コンテナにマウントするディレクトリの指定です。コンテナを停止すると情報が失われるため永続化やファイル操作をしやすくするために利用する事ができます。

- **depends_on（第三階層）**
コンテナの起動順の指定です。ここに記述したサービスの後に起動されるようになります。

# ネットワークについて
docker-compose.yml に記述されたコンテナはローカルのネットワークに接続されて相互に通信が可能です。その際、サービス名で接続が可能となっています。そのためアプリケーション側ではIPアドレスではなくサービス名で接続を作っておくと使いまわしが効くのでオススメです。

# 最後に
今回、最低限の書き方という程度の整理となりました。dockerの環境作りに対して dockerfile、docker-compose があり docker hub のイメージも、どれを使って良いのか迷う事もあります。特にネットワークは迷いどころと思います。LAMP構成やWORDPRESSなど良い感じの docker-compose.yml が一度作れるとカスタマイズして使っていけるので、最低限の項目で動く状態から付け足していくのが良いのではないかと思います。

以上、「docker-compose.ymlの書き方を整理する」でした。
 

