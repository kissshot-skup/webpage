---
title: 【OS自作】OS基礎
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
- 一旦立ち返ってOSとはなにか？から考えよう
- マイコン、SoC、CPUの話
```
----
<br>
■一度立ち返って<br>
自分の頭の中で何となくわかっているつもりでも、具体的に説明しようとするとうまく説明できない。<br>
下回りを勉強しようとしたけど、OSとか、マイコン、SoCいろんな単語がちゃんと説明できるようになりたい。<br>
情報を整理して、以下にまとめてみました。<br>
<br>


----
<br>
■OS：オペレーティングシステム<br>
「基本ソフトウェア」。Word　Excelなどのアプリケーションソフトを応用ソフトウェアと呼ぶのに対し、アプリやデバイスを動作させるための基本となるソフトウェアのこと。OSの例として以下の例のように様々あります。
<br>

```
- Windows
- Mac
- Linux
- Android
- iOS
```
<br>
役割は以下のとおり<br>

```
- H/W管理：
　マウス・キーボード・スピーカー等を管理・制御する。
　デバイスドライバを使って多種多様なデバイスの入出力が可能になる
- マルチタスク・プロセス管理：
  処理工程の順序や、コアの割当などマネジメントの役割を担う
- メモリ管理：
　プログラムされた指示の要求に応じて、メモリの一部をその要求分提供
　競合しないようにし、かつ不要となった時リリースしする役割を担う
- ファイルの管理：
　データに素早くアクセスできるようにする、資源の有効活用、暗号化を実現する
- APIの提供：
　画面表示、入出力、ファイル保存、印刷　のような共通して利用される基本機能を  APIで提供する
```
<br>

----
<br>
■リアルタイムOSと情報系OS<br>
上記Winなどは情報系OSまたは汎用OSと言われ、デスクワークや開発用に使われる。<br>
一方で、要求される時間内に処理が実行できるシステムを構築するためのOSをリアルタイムOS（RTOS）という。組み込み機器向けのOSによく使われます。<br><br>
新人時代に会社の会議で「アールトスがうんたらかんたら」と話していて、「アールトスってなんですか？」と聞いたことがあった。今思うとちょっと恥ずかしかったなぁ。リアルタイムOSって言ってくれればいいのに…と思った記憶。<br>
それはさておき、前回の記事で書いた自作OSはリアルタイムOSです。<br>
<br>
<br>
----
■リアルタイムOSの特徴<br>

```
- 処理（タスク）に優先度が付けられること
- 優先度の高いタスクは、より優先度の低い処理タスクには邪魔されないこと
- 優先度の高いタスクは、低い優先度のタスクの実行権を横取りできること
```
<br>
上記特徴をそなえることによる利点は以下のとおり
<br>

```
- マルチタスク機能による複数機能の並列実行が可能になる
- 保守性・拡張性向上（機能モジュール単位で保守・管理し、アプリ部分の開発に集中できる）→大規模開発に向く
- プログラムの再利用性が高くなる（リアルタイムOSの移植部分のみ（H/Wに依存する部分のみを移植すればよい））
```
<br>

----

■リアルタイムOSの基礎知識・動向<br>
よく聞くμITRONは、RTOSの仕様の一つ。
トロン協会が仕様を定めており、API仕様はオープンになっている。<br>
その他用語説明は以下の通り。
```
- LSI：大規模集積回路（Large Scale Integrated circuit）。半導体集積回路＝ICの中で素子数が1000以上のものを指す←一般論
- RISCマイコン：縮小命令セットコンピュータ（Reduce Instruction Set Computer）
　CPU内部に単純な命令しか持たないかわりに、それらをハードウェアのみで実装して、一つ一つの命令を高速に処理できる。
　ワイヤードロジック（物理的に結線された論理回路）によって全ての命令をハードウェア的に実装
　※組み込み系はRISCが主流。PC以外はこっちと考えて良い
　※Arm社のRISCがトップシェアでAndroid, iPhoneにも採用されている
　
- CISCマイコン：複雑命令セットコンピュータ（Complex Instruction Set Computer）
　CPUに高機能な命令を持たせることによって、一つの命令で複雑な処理を実現
　マイクロプログラムを内部に記憶させることで、高機能な命令が実現できる反面、命令の実行速度は遅くなる
　※PCはCISCが主流。ただしMacは2020年からRISCを採用し始めた
　※IntelはCISCと考えてよい

```
ルネサスマイコンが有名だが、上記Armとの関係性はどうなのだろうか？ちょっと調べてみた。

```
- ルネサスは日立製作所と三菱電機のマイコン部門が統合され、その後NECエレクトロニクスが統合された企業
- ルネサス独自コアのRXファミリが開発されたが、並行してArmコアを取り入れるRenesas Synergyを進め、RAファミリとして、Arm Cortex-M搭載の新32ビットマイコンを開発
```

----
■参考にしたHP<br>
こういう記事は非常にありがたい。。ほんとこれからも何回も確認すると思う。<br>

[世の中には2種類のCPUがある。 CISCとRISCだ。](https://medium.dotsarc.com/%E4%B8%96%E3%81%AE%E4%B8%AD%E3%81%AB%E3%81%AF2%E7%A8%AE%E9%A1%9E%E3%81%AEcpu%E3%81%8C%E3%81%82%E3%82%8B-cisc%E3%81%A8risc%E3%81%A0-a9a69d5d9275)<br>

[値渡しと参照渡しの説明](https://same.blog/2022/01/12/c%E8%A8%80%E8%AA%9E%E5%88%9D%E5%BF%83%E8%80%85%E5%90%91%E3%81%91%E3%81%AB%E5%80%A4%E6%B8%A1%E3%81%97%E3%81%A8%E5%8F%82%E7%85%A7%E6%B8%A1%E3%81%97%E3%82%92%E8%A7%A3%E8%AA%AC%E3%81%97%E3%81%A6/)<br>


[SoCとは](https://qiita.com/lymansouka2017/items/a6e7717821e923ada83c)<br>

[MCUとMPUの違い](https://edn.itmedia.co.jp/edn/articles/1601/26/news018.html)<br>

[DMA(Direct Memory Access)とは](https://uquest.tktk.co.jp/embedded/learning/lecture15-1.html)<br>

[組み込みシステムにおけるリアルタイムOSとLinuxの選択についての考え方](https://www.aps-web.jp/academy/rtos/289/)

----


## [Mainページに戻る](https://kissshot-skup.github.io/webpage)

