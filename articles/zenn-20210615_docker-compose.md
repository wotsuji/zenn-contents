---
title: "docker-compose.ymlの書き方を整理する"
emoji: "😺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Docker","docker-compose","linux","wsl2"]
published: false
---
# はじめに
Dockerは便利です。WSL2のUbuntuでも普通に使えます。Docker for Windows を使わずにUbuntuに対してインストールも可能です。
一時的な環境を作成したりする事も容易です。まずは docker-compose.yml の書き方を整理したいと思います。
※前提としてdockerとdocker-comooseはセットアップ済みという状態を想定しています。

WSL2の場合はDocker for Windowsを使ってDocker環境を作る記事をよく見かけます。
Docker for Windowsを利用するとvs_codeなど統合開発環境と連携できるなどメリットもあると思うのですが
WSL2はDocker for Windowsじゃないとダメという訳では無くLinuxに対する普通のインストールと同様に入れれば使えます。
慣れるまではDockerに関してはコマンドから利用するLinux版でのインストールを推奨したいと思います。

# サンプル

