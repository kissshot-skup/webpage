---
title: 画像生成AI Stable diffusion環境構築編
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
- 画像生成AIを試してみたくローカルで試したがGPU性能足りずに断念
　→Paperspaceで月千円程度レンタルサーバーする方向で環境構築
- 参考記事とコマンドメモ
```
<br>
生成AIで試しに作ってみた画像<br>
<img style="border: solid 2px lawngreen;" src="../images/aitest.png" width="40%"><br>
<br>
<br>

----
### ■環境構築 <br>
GoogleColabが従量課金性になったとのことである程度固定金額で済むPaperspaceで環境構築することにしました。以下記事を参考に。ほんとにまとまってて、詰まるところなかったです。<br>
[おっちゃんでもできたPaperspaceで快適Stable Diffusion Web UI環境](https://note.com/chocolatmars/n/nb0c092b665cd)<br><br>
こちらも参考に<br>
[【2023/10最新版】PaperSpaceのStable Diffusion Web UIを動かす。メリットデメリットの解説](https://kindanai.com/manual-paperspace-stable-diffusion-web-ui/#toc7)<br>
<br>
二つ目の記事で最初作成しましたが、15GBほぼマックス使い切ってしまうので、一つ目の記事のtmpフォルダを使う対策をとりました。<br>
ちなみに、ストレージの容量確認方法は以下<br>
[確認方法](https://moineko.com/ai/paperspace_str/#index_id0)<br>
<br>

----
### ■その他メモ<br>
■生成データをローカルに保存するとき<br>
生成した画像の保存先ファイルの場所は以下<br>
```
/notebooks/stable-diffusion-webui/outputs/txt2img-images
```
<br>
ここで、ZIPファイルにしてローカルPCに保存できるようにする。ターミナルで以下コマンドを実施。
<br>

```
zip -r tempzip.zip /notebooks/stable-diffusion-webui/outputs/txt2img-images
※日付指定したいときは↓
zip -r tempzip.zip /notebooks/stable-diffusion-webui/outputs/txt2img-images/202x-xx-xx
```

<br>
Zipファイルができているので、右クリックでダウンロードできます。<br>
<br>

■不要なファイルを削除するとき<br>
ターミナルを起動して以下を実施<br>

```
/以下でサイズなど確認
du -sch .[!.]* * | sort -h

/消すファイルを決めたら、以下コマンド
rm -r {取得したパス}
※参照パスの時は、./{取得したパス}とすること
```

参考は以下記事<br>

[ファイル/フォルダを削除するためのコードを実行する](https://ma0art.com/paperspace-delete-files/)
<br>
<br>

----
### おわりに<br>
環境が構築できたので、これから色々なモデルを試してみたいと思います。今回はこれにて！<br>

----


## [Mainページに戻る](https://kissshot-skup.github.io/webpage)

