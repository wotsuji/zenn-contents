---
title: "docker-compose.ymlの書き方を整理する"
emoji: "😺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["docker","dockercompose","linux","wsl2"]
published: false
---
# はじめに
dockerは便利です。WSL2のUbuntuでも普通に使えます。一時的な環境を作成したりする事も容易です。ただし docker-compose.yml の書き方に慣れが必要と思いますので整理しておきたいと思います。
※前提としてdockerとdocker-comooseはセットアップ済、dockerfileではなくdocker-composeを利用する事を想定しています。

WSL2の場合はDocker for Windowsを使ってDocker環境を作る記事をよく見かけます。
Docker for Windowsを利用するとvs_codeなど統合開発環境と連携できるなどメリットもあると思うのですが
慣れるまではLinux版でのインストールでコマンドからの使い方に慣れる事を推奨したいと思います。

# サンプル
