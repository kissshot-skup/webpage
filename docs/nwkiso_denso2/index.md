---
title: 【情報処理】RIP,伝送理論について学んだこと2
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
- ルーティングプロトコル（RIP、OSPF、EIGRP）
- メトリック
- ACL
```

----
 <br>
■プロトコルとメトリック <br>
メトリック:ルーティングプロトコルが最適経路を決める値。 <br>
以下プロトコル3種の紹介 <br>
①RIPv1 RIPv2 <br>
　メトリック：ホップカウント <br>
　考え方：経由するルータの数 <br>
　用途：小・中規模 <br>
　計算方法：次のルーターにパケットが渡るときにメトリック＋1 <br>
<br>
②OSPF（Open Shortest Path First） <br>
　メトリック：コスト（経路毎のコストを計算し、最もコストが小さいルートを経由する） <br>
　考え方：インターフェースの帯域幅から算出 <br>
　　　　　例10Mbpsの経路は10、100Mは1、スイッチは1として小さい方を優先 <br>
　用途：中・大規模（EIGRPと違いCISCO以外のルータも使用） <br>
　計算方法：ネイバーテーブルと呼ばれる【隣接ルータ】のIP情報を他スイッチと共有する <br>
　　　　　　（Helloパケットをマルチキャストする） <br>
　　　　　　次にトポロジテーブルを共有し、最終的にグループ全体のトポロジマップを作成する <br>
　　　　　　そこからルーティングプロトコルによる計算が行われ、ルーティングテーブルを作成 <br>
　特徴：IP体系を絞ってメトリックを計算することもできるため <br>
　　　　大規模ネットワークにおける、エリアの細分化により <br>
　　　　ルーティングサイズを小さくでき、CPU・メモリ消費を抑えられる。 <br>
　　　　構成変更による影響度も小さくできる。 <br>
　　　　アクセスコントロールリスト（ACL：Access Control List）により制御する。 <br>
③EIGRP <br>
　メトリック：コスト（経路毎のコストを計算し、最もコストが小さいルートを経由する） <br>
　考え方：帯域幅、遅延を考慮して算出 <br>
　　　　※遅延：パケットを受信してから送信するまでの時間 <br>
　　　　　　　　例スイッチでの遅延＋スイッチ間の遅延 <br>
　用途：CISCO独自仕様 <br>
メトリックの計算式の詳細は下記参照↓ <br>
[https://www.infraexpert.com/study/eigrpz3.html](https://www.infraexpert.com/study/eigrpz3.html)<br>
<br><br>

----
■ACLの動作<br>
上記②のフィルタの仕組みを示す。<br>
ACLの条件は<br>
　・送信元のIPアドレス<br>
　・ワイルドカードマスク<br>
の組み合わせで表現される。<br>
<br>
ワイルドカードマスクとは？<br>
サブネットマスクの反転。サブネットマスクと足すと255.255.255.255になる。<br>
意味としては、0のIPの箇所をフィルタチェック対象とすることとなる。<br>
<br>
例として、IP体系が/24のエリアでは<br>
　サブネットマスク<br>
　255.255.255.0<br>
　ワイルドカードマスクは<br>
　0.0.0.255<br>
<br><br>

----
■OSPF補足<br>
　ルータID：OSPFドメイン内で各ルータを一意に識別する為の番号<br>
	　　　　　重複しないように割り当てる必要あり<br>
　　　　　→設定されていない場合、<br>
　　　　　　ループバックインターフェースの中で最大のIPが設定される<br>
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

