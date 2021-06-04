---
title: "CodePenを使ってHTML/CSS/JSを共有する簡単な使い方"
emoji: "🦉"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["css","html","javascript","js","codepen"]
published: true
---
# はじめに
CodePenというサービスでHTML/CSS/JSを編集してサンプルを作成したりコードを公開する事ができます。画面表示と合わせて作成できるので、一時的に説明する際などに使えます。色々なサイトと連携もされているので画面コードのサンプルを共有する事も可能です。単独で使っても良さそうなCodePenの簡単な使い方を説明したいと思います。

# 会員登録しないで利用してみる
CodePenは会員登録をしなくても利用する事が可能です。ただし「保存」や「公開」などは行えないので自分で作成したHTML/CSS/JSを確認するまでの使い方になります。

CodePen URL
- https://codepen.io/

画面左上の「StartCoding」をクリックすると、会員登録なしに編集を開始する事が可能です。
![](https://storage.googleapis.com/zenn-user-upload/497b10561515d50cce997741.png)

## コードの編集画面は下記のような感じです。
![](https://storage.googleapis.com/zenn-user-upload/87698a3545dba8b56a9cc524.png)
- 左ペインの「HTML」に「body」から先を記述します。
- 中央ペインの「CSS」にStyleタグの中身を記述します。
- 右ペインの「JS」にJavaScriptを記述します。
- 下部ペインに作成したHTMLが画面表示されます。

このままではHTML/CSS/JSは記述はできるのですが保存や公開は行えないため、一時的な編集を行いたいだけであれば問題はなさそうです。

# 会員登録の手順
このままでは保存も公開もできないので会員登録をします。
![](https://storage.googleapis.com/zenn-user-upload/497b10561515d50cce997741.png)
**中央下段の「Sign up for Free」をクリックして会員登録に進みます**

- 今回は「GitHub」を使用して「Sign Up」します。
![](https://storage.googleapis.com/zenn-user-upload/78495957afae482513153fcd.png)

Twitter・GitHub・Facebook・Emailでログインが可能となっているようです。
アカウント連携に少なからずの不安はありますが便利な実装をしてくれています。

無料プランではプロジェクトが１つでファイル10までと制限があるのとコードは全て公開される設定となります。基本的に「プロジェクト」ではなく「Pen」という機能で作っていくのでコードが公開される以外は気にならないかもしれません。
※有料プランであれば非公開設定にする事が可能です。

## GitHub側に画面遷移して許可の操作になります。
GitHubとのアカウント連携の画面に進みますので「Authorized codepen」で許可をします。
※アカウント連携に伴う注意事項は各自にて確認してください。特にCodepenからのRead and write access（読み取りおよび書き込みアクセス）を許可する事となります。

GitHub側で許可するとCodePenにログインがされて簡単なTipsの解説がされますので「Next」を押して説明を終わらせましょう。

これで「SAVE」をクリックする事で保存する事ができるようになりました。
# ZENNにCodePenの埋め込みを試す
ZENNもCodePenに対応しているので記事内に埋め込む事が可能です。試しに埋め込み機能の使い方を確認します。

## ZENNへの埋め込みまでの手順
1. Penにコードを入力してSAVEをクリックします。
2. SAVEすると画面右下にシェア用の「Share」ボタンが出現しますのでクリックします。
3. 「Copy Link」クリックしてクリップボードにシェア用のURLをコピーします。
4. ZENNに埋め込む
- ZENNに埋め込む際の書式は下記のようになります。
\@\[codepen\]\(ページのURL\)

- 実際に共有するURLを入れるとこうなります。
\@\[codepen\]\(https://codepen.io/wotsuji/pen/PopRQLo\)

## ZENNにCodePenの埋め込み
下記がCodePenを埋め込んだ状態です。
「HTML」「CSS」「RESULT」で、それぞれのペインを移動できます。
@[codepen](https://codepen.io/wotsuji/pen/PopRQLo)

ZENNと連携してCodePenを埋め込む事ができました。フロント側のコードを説明するのに役に立ちそうです。

# 最後に
CodePenはJQueryなどのライブラリも豊富に使えるので、バックエンド側のプログラムをやっているとすぐに出てこないHTML、CSS、JavaScriptのコードも試せる状態のサンプルとして用意して共有しておけると思います。

以上、CodePenの簡単な使い方でした。

