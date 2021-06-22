---
title: "WSL2のubuntuのディレクトリをWindowsからエクスプローラーで操作する"
emoji: "🍣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["WSL","WSL2","Ubuntu","Windows","Linux"]
published: false
---

# はじめに
私はLinuxのローカル環境にWindows10＋WSL2でubuntuを使っています。
LinuxからWindowsのディレクトリを操作する場合は「/mnt」にWindows側の各ドライブがマウントされているので簡単に操作ができます。

> Linux：/mnt/c（Cドライブ）

ただし、WindowsからLinuxのディレクトリを操作する際はWinSCPなどで接続していたため不便を感じてました。実はWSL2のディレクトリはWindowsのエクスプローラーから使えます。これを使ってしまうとWSLがより便利になってしまうので紹介したいと思います。

# 検証環境
Windows10 ＋ WSL2 ubuntu 20.04

# WindowsからWSL2のディレクトリへの接続方法

エクスプローラーのアドレスバーに下記を入力する
```
\\wls$
```
※末尾に「$」が入っているため、ネットワークの一覧に表示されないのですが存在しています。

**WSLでインストールしているディストリビュージョン毎に共有フォルダがある状態です**
![](https://storage.googleapis.com/zenn-user-upload/1d53e4bf374762cdc168c989.png)

このディレクトリに対するショートカットをデスクトップなどに作成しておくと良いでしょう。ちなみに、アクセスユーザーは「root」になりますので注意が必要です。

# まとめ
WindowsのエクスプローラーからWSLの中にアクセスできるようになるのでファイルの移動だけではなくファイルの編集も可能で、より便利になりますのでオススメです。


