---
title: "セッションハイジャックをPHPで実際に可能か検証する"
emoji: "🐥"
type: "tech"
topics: ["php", "xss", "脆弱性", "クロスサイトスクリプティング", "セッションハイジャック"]
published: true
---

# はじめに
セッションハイジャックという脆弱性について、机上で知っていたとしても実際に目にした事がありますでしょうか？　一般的にセッションはブラウザの「COOKIE」を利用して実現されます。攻撃者がCOOKIE値を知る事が出来ればセッションハイジャックが成立する機会を与える事になります。

攻撃者がCOOKIE値を知るために使われる脆弱性がXSS（クロスサイトスクリプティング）となり、複数の脆弱性の組合せが必要になるため「攻撃自体を想定しない」というようにセッションハイジャックは甘く見られてしまいがちですが、ログイン系のサイトの場合は偽装ログインが可能となり被害が甚大となるため注意が必要です。

# 検証環境
COOKIEを使い分けるためブラウザを2種類用意します。
１．Fifefox
２．Chrome（アドオン：(EditThisCookie）
※Chromeに下記のアドオンを追加してCOOKIEを編集できるようにしました。
参考：[EditThisCookie（chrome ウェブストア）](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg?hl=ja)

WEBサーバはWindows10 ProのローカルにWSL2でLAMP環境を作成しています。
LAMP環境についてはこちらの記事を参照してもらえればと思います。
https://zenn.dev/o2z/articles/f68d7aea7c075f

# 検証パターン
１．Fifefoxでセッション（COOKIE）を作成する。
２．FifefoxのCOOKIE値を表示する（攻撃者がセッション値を入手したと仮定する）
３．ChromeからCOOKIE値を偽装して接続する（セッションハイジャックを検証する）

# PHPコード
```php
<?php
// 初期処理
session_start();
// セッション値設定
if(!isset($_SESSION['st'])){
    // 値設定
    $_SESSION['st'] = "Session Create ：" . date('Y-m-d H:i:s');
    $_SESSION['count'] = 1;
} else {
    $_SESSION['count'] += 1;
}
?>
<html>
<head></head>
<body>
<h1>Session Hijack Test</h1>
<?php echo $_SESSION['st'] ?><br>
This Session count ： <?php echo $_SESSION['count'] ?><br>
----<br>
<?php echo 'Cookie Session Id ： ' . $_COOKIE['PHPSESSID'] ?><br>
</body>
</html>
```
・説明
セッションが作成された年月日時分秒の保持と表示をする
画面がリロードされた回数をカウントして表示する
COOKIE値を表示する

# 検証
## Fifefoxからセッションを作成してCOOKIE値を表示する
![](https://storage.googleapis.com/zenn-user-upload/wz16mrl1wozpg9vbvrq9a0c3vtzt)
・COOKIE値の表示はリロードが必要なためcount：2になっています。
・COOKIE値「cvk7rf1vf0sfdfkm7gibojrjo5」が取得できました。
## ChromeでCOOKIE値を偽装して接続する
EditThisCookieを使用してCOOKIE値を偽装する
![](https://storage.googleapis.com/zenn-user-upload/yk5fm244be1vmczg6o63l1cstr2l)
セッションハイジャックが成立する
![](https://storage.googleapis.com/zenn-user-upload/vpr2a5kdxfl7zfjraknt9d5ouwnm)

想定よりも簡単にセッションハイジャックが成立してしまいました。XSS（クロスサイトスクリプティング）などによりCOOKIE値を事前に盗む必要がありますが、ログイン系のサイトで攻撃が成立した瞬間のダメージを想像すると気が重くなります。
# セッションハイジャック対策
セッションハイジャックの対策ですが「COOKIE値が盗また事に起因する」ため「XSS（クロスサイトスクリプティング）」が1か所でもあると脆弱性が存在する事に繋がります。第一にXSS（クロスサイトスクリプティング）が存在しないサイトにする事が肝要です。
また、クロスサイトリクエストフォージュリの対策として重要な処理（アップデートなど更新系）に再パスワードの入力を求める事は被害を抑えるために有効と思います。

クロスサイトリクエストフォージュリはこちらを参照
https://zenn.dev/o2z/articles/2eb1c6a3fe8729

# まとめ
特にログインチェックはセッションを使う事がベターであるため、セッションハイジャックされた後の対策は難易度が高くなると思います。そもそもセッションハイジャックが行えない（COOKIE値を盗まれない）ようにXSSなどの対策が必須になると思います。

また、COOKIE値はランダム値なので「[wikipedia：ブルートフォースアタック（総当たり攻撃）](https://ja.wikipedia.org/wiki/%E7%B7%8F%E5%BD%93%E3%81%9F%E3%82%8A%E6%94%BB%E6%92%83)」によりいつかヒットされる事もありえます。
COOKIE値はデフォルトでも複雑な値ですが より複雑な値を使うようにしたり、短時間の大量リクエストを遮断できるようにWAFの導入も考えた方がいいかもしれません。

どちらにしても脆弱性が悪用された時のダメージは計り知れないモノになるため対策は必須であると思います。

以上、セッションハイジャックをPHPで実際に可能か検証する。いかがでしたでしょうか。脆弱性は正しく理解して対策していきたいと思います。