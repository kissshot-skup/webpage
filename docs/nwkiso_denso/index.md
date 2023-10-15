---
title: 【情報処理】RIP,伝送理論について学んだこと
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
- RIPとは
- 伝送方式とは
```

----
 <br>
### ■RIP（Routing Information Protocol） <br>
PCをインターネットに繋げたいと思って、会社のハブ（厳密には“スイッチ”という表現が適当なので、以降スイッチとする）にLANケーブルを繋げると、自動的にインターネットにアクセスできるようになったように見える。 <br>
この時、スイッチがあなたのPCはここにいます！という情報を他のスイッチに伝えてあげている。 <br>
住所がわからなければ、あたなのPCを宛先とした情報が届きようがないからだ。 <br>
自動的に通信ルートの情報をスイッチ間でやりとりする。これを、ダイナミックルーティングプロトコルという。 <br>
RIPはダイナミックルーティングの一つの概念を言う。 <br>
具体的には、自身のルーティングテーブルのコピーを定期的に隣のルータと共有する。 <br>
以下の記事がわかりやすいので展開する。 <br>
[https://www.infraexpert.com/study/routing5.html](https://www.infraexpert.com/study/routing5.html)
 <br>
色々調べていくとディスタンスぺクター型プロトコルというジャンルに含まれているらしいが、ひとまず置いておこう。 <br> <br>

----
 <br>
### ■伝送符号用語 <br>
何かの端末同士を配線した時、どんなふうに信号がやりとりされるか。これは、色々な概念を勉強する必要がある。電気を流したときにON、流さないときにOFFという表現をする。というのは一つの例となるが、もっと高速に通信するための色々な表現がある。ひとまずここでは、用語を抑えていくことにしよう。 <br><br>
・マンチェスター <br>
「0」の時は「高→低」、「1」の時は「低→高」と信号を変化させて伝送する。
<br><br>
・4B5B <br>
4ビットを5ビットのシンボルで表現する。
この5ビットのシンボル中には最低一個以上の1が存在するため、
4ビット以上0が連続しない。
<br><br>
・MLT-3 <br>
Multi Level Transmission-3
「0」の時は変化しない、「1」の時に変化する、という法則で信号を変化させて伝送する。

高中低の3段階の電圧レベルを持っているのが特徴。
<br><br>
・NRZ <br>
Non Return to Zero<br>
ディジタル情報を表現するにあたり、各ビットを表現する電圧が逐一0Vに戻る必要がないもの。

ビットの値0または1に応じて、信号の低または高を決められた電圧で送り出す。
<br><br>
・NRZI <br>
NRZの一種で、Inversion(反転)を特徴とするもの。 <br>

「反転」の解釈方法により、二種類の異なる符号化方法が存在する。
一般にNRZIというと、こちらの方式を言うことが多い。 <br>

電圧の「変化」と「維持」の二種類を、ディジタル情報の0と1に対応づけるもので、FDDIや100BASE-FXなどで使われている。差動(平衡)伝送方式のUSBでも使われている。 <br>

次の二種類があり、どちらも有り得る。 <br>

NRZM(NRZ-M) Mark ‐ 情報が1の場合に電圧を反転、0の場合に維持するもの <br>
NRZS(NRZ-S) Space ‐ 情報が0の場合に電圧を反転、1の場合に維持するもの <br>
実装として多いのは、「0」の時は変化し、「1」の時は変化しない、NRZS(NRZ-S)である。 <br> <br>

Inversion(語順転換)するメリットとしては、受信の際にデータの極性が反転してしまった場合でも、同じ情報が得られるという点である。
 <br>

----
### ■CSMA/CD方式 <br>
複数の端末が接続された通信路において、信号がバッティングして破壊されてしまった時、再送信して正しい信号を認識してもらう必要がある。 <br>色々な方式があるが、その一つがこのCSMA/CD方式。 <br><br>
色々な信号が混在する信号を感知 (Carrier Sense) しフレーム伝送を行い、フレームが衝突を検出 (Collision Detection) するとランダムな時間を待ち送信を開始する。この方法で、1本のケーブル上 (1つのネットワークの媒体上) を
複数のノードがお互いにアクセス (Multiple Access) できる。 <br>
 <br>

最近では、スイッチが上手いことやってくれるので信号の衝突を考えなくてもよくなりつつある。 <br>
（ただ、産業用通信だったりは、バス型の接続も考えなければいけないので、基礎知識として必要な概念のため、抑えておく必要がある） <br>
 <br>
もともと同軸ケーブル（1本の導線）での通信で用いていた。 <br>
CSMA/CDは半二重(half duplex)の通信において使用する通信方式であり、
全二重 (full duplex) の通信でCSMA/CDは使用されない。 <br>
スイッチングハブに接続されたノードはいつでもデータの送受信が可能。
※リピータハブを使った場合は衝突する。下記参照 <br>
[http://www.osssme.com/doc/funto106-no20.html](http://www.osssme.com/doc/funto106-no20.html)
<br>
<br>
### ■TCP（Transmissyon Control Protocol）<br>
Web、メール、FTPなどデータを確実に送り届けたい通信で使われます。<br>
TCPは、データをセグメントに分割して送信するだけでなく、確実に送り届けるために送信速度を調整し、上手く届かなかったデータがあれば再送するように手配します。<br>
<br>
<br>
----

### ■リピータハブの応用面白かった記事 <br>
[http://www.osssme.com/doc/funto106-no20.html](http://www.osssme.com/doc/funto106-no20.html)
 <br>

----


## [Mainページに戻る](https://kissshot-skup.github.io/webpage)

