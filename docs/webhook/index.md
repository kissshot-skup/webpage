---
title: 【情報処理】AWSでwebhookの受信を実装する（API Gateway＋Lambda）
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
この記事にはこんなことが書かれています。
- webhookとは
- API Gateway
- Lambda
```

----
 <br>
■モチベーション <br>
客先システム導入時に担当者から「ある処理の完了通知をwebhookで投げることができる」 <br>
と連絡をうけた。webhookとは何かから勉強することになったが<br>
AWSでその受け皿をつくることができたのでその軌跡を書く <br>
<br>
＜webhook概要＞ <br>
あるアプリケーションから別のアプリに対して、リアルタイムな情報提供を実現するための仕組み。 <br>
例えばインターネットであるホームページを見るときには、自身のPCは「この情報くれよ」とあるサーバーに対して問合せをして、サーバー側から「お前は誰？」とか「誰か確認できたからこの情報あげるね」とかをやり取りしている。 <br>
それに対してWebhookは、何かイベント発生をしたら、決められた情報を通知するだけの仕組みで、送信側・受信側ともに効率のいい方法です。 <br>
<br><br>

----
■webhookをもう少し詳しく<br>
以下資料がわかりやすかったです↓ <br>
[WebhookのWeb APIとの違い 〜イベントと通信に着目してみた〜](https://qiita.com/kuwazzy/items/fdf363cc1caee9a23686)<br>
[データ連携(Webhook)](https://webiot.io/docs/console/datalinkage/)
<br>
webhookは<br>
　・http(s) GET　<br>
　・http(s) POST　<br>
の組み合わせを使ってイベント駆動で情報を送受信することがわかりました。<br>
<br>
ボディと呼ばれる、HTTPの中身に情報をいれて送受信しますが<br>
JSONと呼ばれる形式で書くのが一般的なようです。<br>
これはWebhookに依らずよく使われる形式で<br>
非常に見やすく簡単な構造で以下のような感じです<br>
<br>
```
{
  "id":"{id}",
  "value":"{value}",
  "unit":"{unit}"
}
```
"id"部分をキーと呼び、“｛ほにゃらら｝”をバリューといいます
<br>
キーは何か概念を表すもので、バリューはその値です。非常にシンプルですね。
<br>
例えば、ある温度センサーから定期的に温度の値の値知する仕組みを作って、JSONでやり取りしましょうとなったらこんな感じでしょうか。<br>
```
{
  "id":"{1}",
  "area":"{nagoya}",
  "temperature":"{28.5}"
}
```

----
■webhookの実装<br>
　<br>
<br><br>

----
■リンクアップ	　　<br>
DR（Designated Router）：LSAの交換を取りまとめる代表ルータ<br>
　　　　　　　　　　　　　プライオリティ値の最大で決まる<br>
BDR（Backup Designated Router）：DRにバックアップとして動作する<br>
Helloパケット：10秒毎にHelloパケットを投げて、40秒間届かなかった場合にリンクダウンしたと判断<br>
　　　　　　　　デッドインターバルという。<br>
LSU（Link State Update）：新しく接続された機器たDRとBDR宛に送るモノ<br>
　　　　　　　　　　　　　　DRが全体に通知する。<br>

<br><br>

----


## [Mainページに戻る](https://kissshot-skup.github.io/webpage)

