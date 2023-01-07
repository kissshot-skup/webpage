---
title: 【情報処理】ネットワーク基礎知識のメモ5
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
- TLSとは
- サーバ稼働率の計算方法
- DNS（Domain Name System）
- DNSレコード
- 
- 
```
----
今回もネットワークの基礎をまとめていきます。<br>
<br>

----
■TLS(Transport Layer Security)<br>
・SSLのこと。SSL3.0→バージョンアップしてTLSとなった安全性の高い通信を行うプロトコル<br>
・一般的には「SSL」や「SSL/TLS」のような表現<br>
・公開鍵認証や共通鍵暗号、ハッシュ化などの機能を提供<br>
・公開鍵は電子データにつき、ICカード等に封入も可能<br>
<br>

----

■サーバ稼働率の考え方<br>
・直列接続と並列接続がある<br>
・考え方は以下のとおり<br>
<br>
Aシステム稼働率：x<br>
Bシステム稼働率：y<br>
<br>
直列接続：x * y<br>
（どっちかが壊れたら終わりなので単純に掛け算）<br>
例：x=0.9 y=0.8の時システム稼働率は0.72<br>
<br>
並列接続：1－((1-x)*(1-y))<br>
（両方壊れなければOK→Aシステムが壊れる確率とBシステムが壊れる確率の反対）<br>
<br><br>

----
■DNS、DNSレコード<br>
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

