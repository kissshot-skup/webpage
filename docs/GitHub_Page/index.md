---
title: GitHub PageによるHP公開方法について
---


```
この記事にはこんなことが書かれています。
‐ GitHub PageによるHP公開方法について
‐ WordPressより簡単、サーバ管理費かかりません
‐ マークアップ言語で書かれたファイルの編集などの知識は多少いるけれど、そんなに難しくない！
```

## まずは全体の流れを把握しよう
下記の記事をサラっと眺めて何となく何が必要かを感じてみましょう。
それが一番の早い方法かと思います。何となくで大丈夫です、わからないところは下記で解説します。
- [GitHubを使って3分でHPを公開する](https://qiita.com/budougumi0617/items/221bb946d1c90d6769e9)
- [GitHub Pageを用いたHP作成](https://netchira.github.io/blog/githubpages/GettingStarted.html)
- [1分でできるGitHub Pagesの作成方法](https://iwb.jp/github-pages-how-to-create/)

一つ目のリンクは、Quittaで最もLikeが多い記事です。つまり人気がある記事です。
ただ、私がGitHub初心者ということもあり、上記記事だけでは、つまるポイントが何点かありました。
特に難しくさせていると感じた点は下記です。
・GitHubが何かをわかっている＆操作も慣れている前提
・コマンド操作ができる人前提
・Macユーザ向けの操作方法で書かれている記事が多い

なので、上記でわからないところを補足しつつ下記に説明していきます。
この段階でわかるべきことは
「GitHubに登録する→GitHub PageというアプリでHPを公開する設定にする」
の二つの手順でHPが作成できるということです。

ではそれぞれやっていきましょう。

### 1.GitHubの登録
下記の記事を参考にGitHubのユーザ登録を行いましょう。
いくつか記事がありますが、画像付きで一番わかりやすかったです。
- [【最新版】GitHubアカウントの作成方法を画像付きで解説！](https://pengi-n.co.jp/blog/github-account/)

そもそもGitHubって何？というのを知りたい方は下記を参照ください。
ソフト設計に関わる方は避けては通れないバージョン管理ツールの一種です。
- [GitHubとは？特徴からアカウント登録方法まで徹底解説！](https://udemy.benesse.co.jp/development/system/what-is-github.html)


### 2.GitHub Pageの設定
次のステップでHPを作成していきます。
まず、下記記事のリポジトリの作成というところまで進めてみてください。
- [自分で作ったWebページをインターネット上に公開しよう！](https://prog-8.com/docs/github-pages)

上記記事でファイルのアップロードの説明がありますが、もっと簡単な方法があります。
下記記事を参照してGitHub Pageをセッティングしてみてください。0タイピングで、作成できます。
- [GitHub Pagesでプロジェクトホームページを作る。15秒で。](https://qiita.com/kaitoy/items/509ccefb1b31d80ba3f1)


### 3.HPの確認
　無事2．まで完了したら作成したHPを確認してみましょう。
　上記2．で作った「https://アカウント名.github.io」をWebページのバーに入力してみてください。


### その他メモ
　以下は紆余曲折あって、上記以外で対応したときにハマったポイントです。
　読み飛ばし可能です。

　複数記事ではGitHubとPelicanを使う方法が紹介されていますが
　Winユーザの私はハマりました。。。下記特殊対応が必要です。
- [**Winユーザの方の記事**](https://qiita.com/ogrew/items/ecef0a4700d5bd4d875d)
- [makeが通らない](https://www.ainoniwa.net/pelican/wp/1072.html)

　makeってなんだっけ？となったので下記で調べたりしました。
- [makeについて](https://qiita.com/hotoku/items/6e50c9f8864e98468ac7)

　Pelicanを使うともっと簡単にHPをアレンジできる様子
- [Pythonの静的サイトジェネレータ"Pelican"でお手軽にブログをはじめる手順](https://jpdebug.com/p/2538708)

　3.の確認方法として、他にローカルホストを使う手もある。
　http://localhost:8000/で確認する方法は下記を参照する。
- [ローカルホストでHPを確認する](https://qiita.com/higuma/items/b23ca9d96dac49999ab9)
- [作ったHP](https://kissshot-skup.github.io/webpage/)

  Markup言語で画像を挿入する
- [GitHubでREADME.mdにレポジトリ上にある画像ファイルを表示するアレコレ](https://qiita.com/hibara/items/f343b5ec2f48d46adfe6)
  アイコン集
- [拝借させていただいたアイコン集](https://boxicons.com/)




## [Mainページに戻る](https://kissshot-skup.github.io/webpage)

