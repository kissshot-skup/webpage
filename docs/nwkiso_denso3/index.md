---
title: 【情報処理】ネットワーク基礎知識のメモ3
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
- Active Directoryとは
- DHCPとは
- NATとは（プライベートIPアドレス・ループバックアドレスの復習も）
- VLANとは
- ルータオンアスティック
- ルータとL3スイッチの違い
```
----
今回もネットワークの基礎をまとめていきます。<br>
<br>
### ■Active Directory<br>
・IDやパスワード管理を行う概念<br>
・アクセス権限の設定と管理ができる<br>
イメージ:Active Directoryを使えば、出張などでどこにいっても場所を選ばず会社システムにアクセスできるようになる<br>
<br>

----
### ■DHCP（Dynamic Host Configuration Protocol）<br>
・サーバ<br>
・DHCPサーバ⇒スイッチ⇒各PC（DHCPクライアント）の構成で、DHCPサーバによってクライアントはIPアドレス、サブネットマスク、デフォルトゲートウェイなどパラメータを自動的に取得可能となる<br>
・上記パラメータはリース（デフォルト24時間）される<br>
・DHCPの動作は4段階<br>
```
　1：DISCOVER（クライアントからブロードキャストでDHCPサーバを検出する）
　2：OFFER（サーバ⇒クライアントへIPアドレスを予約して送信）
　3：REQUEST（クライアント⇒サーバへIPアドレスを受け入れる意思を示す）
　4：ACK（サーバ⇒クライアントへクライアントの要求に応答する）
```
<br>

----

### ■NAT Network address Transtration<br>
・ルータに設定するもの<br>
・ルータがインターネットに出ていくときにプライベートなIPアドレスをグローバルなIPアドレスに変換する<br>
<br>
```
＜プライベートIPアドレスの範囲＞
①10.0.0.0 ～ 10.255.255.255	    （10.0.0.0/8）
②172.16.0.0 ～ 172.31.255.255	  （172.16.0.0/12）
③192.168.0.0 ～ 192.168.255.255 （192.168.0.0/16）
```
<br>
基本知識（復習）<br>
①～③はクラス分類によって定義されている<br>

```
クラスA：頭が0 		0xxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx 
		アドレス範囲が0.0.0.0～127.255.255.255
クラスB：頭が10		10xxxxxx xxxxxxxx xxxxxxxx xxxxxxxx
		アドレス範囲が128.0.0.0～191.255.255.255
クラスC：頭が110	110xxxxx xxxxxxxx xxxxxxxx xxxxxxxx
		アドレス範囲が192.0.0.0～223.255.255.255
```
<br>
＜参考＞<br>
[参考HP](https://atmarkit.itmedia.co.jp/ait/articles/0301/17/news003.html) 
<br>
覚えるのが大変な場合、以下HPを参考にすると少し楽かもしれません<br>
[参考HP](https://mophie-blog.com/2022/02/18/how_to_remember_ip_class_global_and_private/) 
<br>
更に豆知識<br>
よく使われるローカルループバックアドレスは127.0.0.1<br>
厳密には127.0.0.1～127.255.255.254の中で割り当てられる。<br>
※127.0.0.0はネットワークアドレスを表し、127.255.255.255はブロードキャストアドレスとなるため。<br>
<br>
ループバックアドレスとは<br>
機器自身に設定され、危機がダウンしない限り有効なIPアドレス<br>
使用例）<br>
自分のPCでwebサーバを稼働している場合に、ブラウザから自身のPC内のWebサーバに対してこのループバックアドレスを指定してアクセスできるかの確認を行う。<br>
ブラウザのアドレスバーにhttp://127.0.0.1などと入力してアクセスする<br>
<br>
<br>

----
### ■NATの種類<br>
①スタティックNAT<br>
変則規則が永続的に登録される。<br>
組織が外部NWに対してWebやFTPサーバなどを公開する目的で使用<br>
内部ホスト外部ホストどちらからでも接続を開始できる<br>
<br>
②ダイナミックNAT<br>
グローバルアドレスをNATプールに登録しておき、内部のローカルユーザが同時にインターネットにアクセスできるのはプールに登録された数まで<br>
例）<br>
NATアドレスプールが1.1.1.1～1.1.1.4だった場合、4台までインターネットにアクセスできる<br>
<br>
③PAT（NAPT）<br>
1つのグローバルアドレスを複数の内部ローカルアドレスで共有する<br>
NATテーブルに、ポート番号も含めて登録しておくことで、同じグローバルアドレスを複数のローカルユーザが使用できるようにしている<br>
例）<br>
ローカルユーザ10.1.1.2：ポート番号50000と10.1.1.1：51000のユーザがいた場合、前者はグローバルアドレス1.1.1.1：50000、後者は1.1.1.1：51000を使う<br>
<br>
<br>

----
### ■DHCPサーバの役割<br>
・ユーザのPC（クライアント）にIPアドレスを払い出す。<br>
<br>

----

### ■VLAN<br>
ルータなしでスイッチのポート毎にネットワークを分けることができる。<br>
例えば、スイッチのポート1～3をVLAN1、ポート4～6をVLAN2と設定すれば、VLAN1と2で個別のネットワークとなる。<br>
通常、スイッチは受け取ったパケットを全ポートへ転送（フラッティング）するが、VLANを分けていれば、転送するネットワークを絞ることがえでき、転送効率が向上する。<br>
スイッチに割り当てたVLAN IDを変更するだけで違うネットワークにアクセスが可能になる。<br>
ポート1をVLAN1で営業部が使っていたが人が移動になって別の部（VLAN2）の人が使うことになった場合、ポート設定をVLAN2に変更するだけで別の部のネットワークにアクセスが可能になる。<br>
<br>
※デフォルト設定ではすべてのポートがVLAN1に所属している<br>
<br>
<br>

----
### ■VLANの種類<br>
①アクセスポート<br>
1つのI/Fに1つのVLANを設定する方式<br>
<br>
②トランクポート（タグ付きVLAN）<br>
1つのI/Fに複数のVLAN設定する方式。<br>
例えば、スイッチ同士をトランクポート方式で、各ポート毎のVLAN設定を次のスイッチに教えてあげる<br>
トランクポートだけがタグをつけたりとったりできる（アクセスポートではタグをつけたりできない）<br>
タグが付かないVLAN（初期設定ではVLAN1）はネイティブVLANと呼ばれる。タグがないものが来たらVLAN1に転送する。<br>
<br>　
シスコスイッチはデフォルトでDTP（ダイナミックトランキングプロトコル）の設定になっていて、対向機器のポートとネゴシエーションを行うようになっている。<br>
autoの設定の場合、対向先の設定に合わせる（トランク設定ならトランクポートになる）<br>
<br>

----
### ■ルータオンアスティック（Router on a stick）<br>
本来はVLANが増えるたびにルータから別のLANを這わせる必要があるが、拡張性がなくなるので、1本のLANで複数のVLANと区別するための方式。<br>
<br>
VLAN1のIPが192.168.1.0/24<br>
VLAN2のIPが192.168.5.0/24<br>
の場合、ルーティングテーブルは、<br>
192.168.1.0/24 connected fa0/0<br>
192.168.5.0/24 connected fa0/1<br>
であるところ、Router on a stickの考え方を適用して<br>
ルーティングテーブルは、<br>
192.168.1.0/24 connected fa0/0.1<br>
192.168.5.0/24 connected fa0/1.5<br>
というに定義して、VLAN毎にルーティングする<br>
<br>
《参考》<br>
以下URLの説明が分かりやすかった<br>
[参考HP](https://www.infraexpert.com/study/vlanz8.html) 
<br>
<br>
### ■ルータとL3スイッチの違い<br>
改めてL2、L3、L4スイッチの違いが気になった。<br>
そして、なんとなくL3スイッチはルータ相当というイメージがあるが、違いは何か気になった。<br>
<br>
L何とかというのは、レイヤー何とかという意味であり
OSI参照モデルの層を意味している。<br>
L2スイッチは、データリンク層<br>
L3スイッチは、ネットワーク層<br>
L4スイッチは、トランスポート層までをサポートしていると考えてよい<br>
<br>
役割分担は以下。<br>
```
L2スイッチ：各ポートに接続されたPCなどのデバイスとMACアドレスを紐づける
L3スイッチ：IPアドレスベースでのデータの中継が可能
L4スイッチ：IPアドレス以外にTCP／UDPのポート番号による中継が可能。複数サーバへの負荷分散やセッションの最適化を行える
```
<br>
では、ルータとL3スイッチの違いは？<br>
```
・ルータはLANとWANの境界に設置するのに対して、L3スイッチはLAN内に設置する
・ルータはNATの機能を備えている
・ルータはVPNや外部からの通信を制限する機能がついている
```
《参考》<br>
[参考HP](https://qiita.com/yoyoyo_pg/items/fef3ddeb05989d03bbef) 
<br>
<br>
### ■VLANタグベース以外の優先度制御<br>
DSCP：Differentiated Services Code Point<br>
パケット内IPヘッダ内のToSフィールド6bitで優先度を制御する<br>
[参考HP](https://www.itbook.info/study/qos11.html) 
<br>
<br>
<br>
今回はここまで<br>

----


## [Mainページに戻る](https://kissshot-skup.github.io/webpage)

