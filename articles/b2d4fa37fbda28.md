---
title: "TortoiseGit「git did not exit cleanly (exit code 128)」が発生した時の対処"
emoji: "🦔"
type: "tech"
topics: ["git", "github", "windows10", "tortoisegit", "証明書エラー"]
published: true
---

# 概要
Windows10 + github ＋ TortoiseGit　の組み合せで使っていたところ急に「git did not exit cleanly (exit code 128)」というエラーが発生してCommitに失敗して、Fetchも出来ない状態となってしまいました。
### 状況
- 前日にGithubへのCommitを行っているが普通に使えている状態であった
- ユーザー名・パスワード等は変更していない
- Widnows10のフリーズや強制シャットダウンも発生していない
# エラーメッセージをGoogleで翻訳してみる
git did not exit cleanly (exit code 128)
> gitが正常に終了しませんでした（終了コード128）

前回のTroiseGitが正常終了していないと発生するのかな？
しかし、Windows10を再起動をしても変わらず。
## Google検索
Googleでエラーメッセージを検索すると
・TroiseGitのターミナルや証明書にエラーがある時に発生する
・パスワードが間違っている発生する
・TroiseGitを再インストールしても改善しない

というような情報が出てきます。
## 対処として
１．TroiseGitのターミナルを別のモノに切り替える
２．TroiseGitの証明書は「Windows 資格情報」に記録されているので
　「Windows 資格情報」の「Git Hub」の証明書を一度削除して再登録させる
３．TroiseGitの証明書チェックを無効にする

という方法があるようです。
# 実際にやったこと
「１．」のターミナルを切り替えるのは後々で変な事になる気がする。
「２．」は「Windows 資格情報」を削除するのは面倒ですし、これは再発する気がする。
ということで「３．TroiseGitの証明書チェックを無効にする」にしてみます。
:::message alert
証明書は 通信のなりすまし や 改ざん を検知する役割もあるため、商用利用などの場合は「１．」か「２．」の試す事を強く推奨します。
:::
# TroiseGitの証明書チェックを無効にする 設定手順
１．右クリックメニュー「TortoiseGit」⇒ 「Settings」
２．左メニューの「Git」を選ぶ
３．「Git uses the concept of a hierarchical ...」という警告が出るので「OK」をクリック
　※上位の設定を変更すると下位の設定は上書きされるます。というメッセージのようです。
４．「Edit global.gitconfig」をクリック
　テキストエディタ（私はメモ帳でした）で設定ファイルが開かれます
５．下記の記述を追加して保存する
```
[http]
	sslVerify = false
```
※再起動等は不要で設定が反映されます。

Commitを試したところエラーが解消されました。
# 最後に
今回「証明書のチェックを無効にする」という対策をしたので再発しなくなると思いますが「パソコンを買い替える」「他の人に発生してサポートする」は想定されると思います。でも、その時は忘れてしまっていると思う次第。この記事が思い出される事を祈ります。

以上、「TortoiseGit「git did not exit cleanly (exit code 128)」が発生した時の対処」でした。ツールも正しく理解しないとですね。
