---
title:【HTML】検索フォームをつくろう
---
<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-2844921131740253"
     crossorigin="anonymous"></script>
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-H1234VX5NE"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-H1234VX5NE');
</script>



```
この記事には以下ネットワーク基礎知識が書かれています。
- ホームページに検索フォームを追加する方法
- HTMLの基礎的な話をおさらい（今までなんとなくでやってきたつけが…）

```
----
ホームページの記事も増えてきて、自分でもどこに何を書いたのかわからなくなってきました。<br>
カード形式に記事を配置して、技術系の記事や趣味とか分類してソートできるようなボタンを配置したりとかしてきましたが、分類はわかるんだけどあの話ってどこに書いたっけ…というのがちらほら。<br>
よくある検索フォームを作る奮闘記です。参考になれば。<br>

----
■検索フォームを作る方法<br>
色々とググってみて、以下構文をHTMLファイルに埋め込めばなんとかなりそう。と分かりましたが、初心者にとってどの行が何をしているのかさっぱりです…。まずは少し構文理解を進めてみることに。<br>

```
<form method="post" action="URL" method="get">
	<div>
		<label for="search">検索する</label>
		<input type="search" name="s" placeholder="キーワードを入力">
	</div>
	<input type="submit" value="検索する" />
</form>
```
----

■そもそも "form"とかってなんだっけ？<br>
今まで適当にやってきたツケが回ってきました。<br>
恥ずかしながら、上記を調べていたときに、divで記載してあったりformで記載してある記事があり違いがわかりませんでした。<br>

HTMLのタグと呼ばれる構文を調べてみると以下記事がわかりやすかったです。<br>
[HTMLのよく使うタグ一覧！この15個さえ押さえればOK！](https://zero-plus.io/media/html-tags-and-usage/)<br>

上記記事で、divタグはわかりました。formタグは載っていませんでしたが、タグの一種で、送信フォームなどを作るタグのようです。独自の使い方があるようで、少し学習する必要がありそうです。

----
■formの使い方を調べた結果<br>
以下の記事を参考にしました。特に２つ目の記事は好みの記事です。<br>
[【HTML入門】formタグを使ってフォームを作る方法を1から解説](https://www.sejuku.net/blog/81862)<br>
[HTMLのフォーム（form）コンプリートガイド](https://catnose.me/learning/html/form)<br>

```
・methodはPOSTかGETを指定する項目で、サーバに対して送信するか受信するかを決める
　検索フォームとしては検索したいワードを問い合わせるのでPOSTが正しい
・actionは問い合わせ先のサーバ：検索フォームとしてはgoogle先生か自身のホームページ
・inputは入力欄をつくるコマンド：検索フォームとしては検索
・labelは入力欄の項目名を表示させるコマンド
・nameは入力されたデータの名前を決めるもの
　入力された値が、どの入力欄に対応しているのかをサーバー側が分かるようになる
```
と分かったところで、以下に編集してHTMLに埋め込みました。<br>

```
<form action="https://kissshot-skup.github.io/webpage/#" method="post">
  <input type="search" name="search" placeholder="キーワードを入力">
  <input type="submit" name="submit" value="検索">
</form>
```
<br>
出力結果はこんな感じ↓<br>
<img src="../images/kensaku1.png" width="80%"><br>
<br>
<br>
適当な文字列を入力して検索ボタンを押したものの、以下エラーが。<br>
<img src="../images/kensaku2.png" width="80%"><br>
405エラーをググると“Webサーバで起きるエラーの種類の一つで、クライアントが指定した要求の種類が受付不可に指定されていることを示すもの。”とあります。<br>
もう少しうまくいかない理由を考えてみました。
<br>
<br>

----
■<br>
・IPアドレスとドメイン名(google.comなど)を紐づけてくれるシステム<br>
・DNSサーバには役割が違うものが2つあり、以下①②。<br>
```
①フルサービスリゾルバ：問い合わせに対し答えがわかれば答える、わからなければ別のDNSサーバに代わりに問い合わせしてくれる。過去問い合わせしたことのあるモノは、キャッシュに保存しておき、次回以降は答えられるようにしておく仕組みがある。

②権威DNSサーバ：フルサービスリゾルバが知らない場合に問い合わせを受けるサーバ。自分が管理している情報の中に答えがあれば答え、他サーバに委託していれば委託先を答える。全然わからない時は不明と答える。
```
[参考:DNSサーバの種類](https://wa3.i-3-i.info/word1288.html)<br>
<br>
<br>
・ゾーンファイル：上記権威DNSサーバが管理しているファイル。IPアドレスとドメイン名の対応が書かれた表<br>
・DNSレコード：ゾーンファイルに書かれた1行ごとの情報<br>
代表的なレコードは以下の通り。<br>
```
①SOAレコード
ゾーンファイルの先頭に書かれる。管理者情報などの管理を行うDNSサーバを定義する。Start of Authorityの略。
②Aレコード
ドメイン名⇔IPアドレス(IPv4形式)
③AAAAレコード
ドメイン名⇔IPアドレス(IPv6形式)
④MXレコード
ドメイン名⇔メールサーバ
⑤NSレコード
“このドメイン名はこのネームサーバに確認するように”と定義する
⑥CNAMEレコード
ドメイン名の別名を定義するレコード。このドメイン名とこのドメイン名は同一と伝えるもので、エイリアスとも呼ばれる。
```

[参考 ゾーンファイルについて](https://wa3.i-3-i.info/word12283.html)<br>

注意：上記AやAAAAレコードの表現をみるとドメイン名とIPアドレスは1対1のように見えてしまうが、DNSサーバは、ホスト名：IP＝1:n,n:1どちらの設定も可能。<br>
【利用ケース】<br>
```
・1:n ：1つのホスト名に複数のIPを対応させて負荷分散したい
・n:1 ：FTPサーバWebサーバSMTP、POPサーバなど1台のサーバ内で運用されている場合はAレコードやCNAMEレコードの記述で複数のホスト名を1つのIPアドレスに関連づける
```
《補足》
DNS amp攻撃<br>
・脆弱性のあるDNSサーバへ再帰的な問合せをすることでサービス不能とする攻撃。分散型サービス妨害(Distributed Denial of Service: DDoS)攻撃の一種。対策として、利用可能なホストのIPアドレスの範囲を設定するなど、DNSキャッシュサーバが不要なクエリを拒否するようにアクセス制限を施す必要がある。
<br>
<br>
----
■SMTP(Simple Mail Transfer Protocol) POP(Post Office Protocol)<br>
・SMTP:メール送信プロトコル<br>
・POP：メール受信プロトコル（ポストオフィス＝郵便局プロトコル）<br>
・いずれもOSI参照モデル第7層アプリケーション層のプロトコル<br>
SMTP・POPの手順は以下<br>

```
SMTPの手順
①作成したメールをメールサーバへ送信
②送信元メールサーバから受信側メールサーバへ転送
ここまでSMTP。以降POP
③受信者のメールアプリが受信側メールサーバへチェック
④受信側のメールサーバから受信者へメール送信
```
これだと、悪意のある利用者がメール送信し放題となるため、以下対策が考えられた。<br>
受信側：POP3：利用者名とパスワードを設定して認証した後に受信する方式
以下手順を踏む
```
①メールアプリがサーバへTCP(ポート110番)で接続
②ユーザとパスワードをサーバがチェックする
③認証後にメール受信手順を実施
```

送信側：POP before SMTP：利用者がメールをSMTPで送信する前に、POPによる認証を行う方式。つまり、一旦メールサーバと上記POP3の認証を行ってメール受信をした後にメールが送信できる。<br>
<br>
POP before SMTPの利点は、POP3ができるシステムである端末であれば、利用者の端末の開発要素なしで適用できること。注意点は、サーバ側は送信元のIPアドレスを記憶したうえで記録したIPアドレスだけをSMTPサーバで利用可能にする仕組みであることから、同一のグローバルIPを利用しているなどIPを偽造されると不正メールの送信を許可してしまう可能性がある<br>

<br>
<br>
以下でwiresharkでパケットの中身を見て学ぶやり方が書かれていました。パスワードやらが丸見えな場合があるかもなのでちょっと衝撃です、一回どこかで試してみたいです。<br>
[メールのやり取りをキャプチャみよう](https://www.itbook.info/network/pop3.html)<br>

----
■OpenFlowとSDN<br>
・SDN：Software Defined Network：単一のソフトウェアによりネットワーク機器を集中的に制御して、ネットワーク構成や設定などを柔軟＆動的に変更可能にする技術の総称<br>
・機器の「データ転送機能」と「制御機能」を分離して、制御機能をもつソフトウェア（SDNコントローラと呼ぶ）が集中管理をする体系<br>
・OpenFlowとは、SDNを実現する技術の1つ。Google等が参加する団体ONF(Open Networking Foundation)が標準化を進めている<br>
<br>
<br>
----
■プロキシサーバ<br>
・Webブラウザ（Googleなど）であるホームページを閲覧したい場合に、Webサーバへ問合せを行うが、この時に仲介してくれるサーバ。<br>
・メリットは、身元を隠せることと、キャッシュを上手く使えばアクセスが早くなること<br>
・リバースプロキシは、Webサーバ側におかれるプロキシサーバのこと（リバース：逆）。外部インターネットからサーバへアクセスされる通信を中継する。Webサーバの身元を隠せる上、負荷分散に貢献する。<br>

<br>
<br>

[リバースプロキシとプロキシの違いとは？それぞれのサーバーの仕組みは？](https://eset-info.canon-its.jp/malware_info/special/detail/201021.html#:~:text=%E3%81%93%E3%82%8C%E3%81%BE%E3%81%A7%E8%A6%8B%E3%81%A6%E3%81%8D%E3%81%9F,%E3%81%AE%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E3%82%92%E4%B8%AD%E7%B6%99%E3%81%99%E3%82%8B%E3%80%82l)<br>

----
■WebDAV(Web-based Distributed Authoring and Versioning)<br>
・HTTPを拡張したプロトコルを使用して、Webサーバ上のファイルを管理する仕組み<br>
・メリットは、FTPと比較してブラウザ上で操作できることやSSLによるセキュアな通信コネクションを使用できること<br>
・ファイアウォールなどでFTPが使用できない場合に使用する<br>
<br>
<br>

<!--ひな型
----
■<br>
・<br>
・<br>
・<br>
<br>
<br>
[https://www.infraexpert.com/study/tcpip21.html](https://www.infraexpert.com/study/tcpip21.html)<br>
-->


<br>
<br>
今回はここまで<br>

----


## [Mainページに戻る](https://kissshot-skup.github.io/webpage)

