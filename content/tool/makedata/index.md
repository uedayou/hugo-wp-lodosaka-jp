---
title: LODを作る
author: webmaster
type: page
date: 2015-01-20T00:45:36+00:00
---

Linked Open Data(LOD)を作るには、
[LinkData.org][1]
を使う方法と、
[Open Refine][2]
とそのエクステンション
[GRefine RDF Extension][3]
を組み合わせて使う方法があります。

### [LinkData.org][1]

[LinkData.org][1]
は、独立行政法人理化学研究所が開発、一般社団法人リンクデータが運用するLOD作成支援サイトです。  
Excel や Googleスプレッドシートで作成した表形式のデータを、
[LinkData.org][1]
のサイト上で簡単にRDFデータを作成可能で、作成したRDFデータをすぐにWeb上で公開することができます。  
Googleスプレッドシートを使う場合、Webブラウザのみで全ての作業を行うことができます。

詳しい使い方は、
[LinkData.org][1]
の
[チュートリアルページ][4]
、または以下の資料をご覧ください。

#### LOD技術の概要とLinkData.orgを用いたLOD公開

{{< slideshare id="38278848" >}}

#### LODオープンデータのつくりかたと項目名のつけかた

{{< slideshare id="42456061" >}}

### Open Refine + GRefine RDF Extension

- Open Refine<

<http://openrefine.org/>

- GRefine RDF Extension

<http://refine.deri.ie/>

[Open Refine](http://openrefine.org/)
は、CSV、TSV、Excel、Googleスプレッドシートなどさまざまな形式のデータを自由に整形することができるソフトウェアです。この
[Open Refine](http://openrefine.org/)
にエクステンション
[GRefine RDF Extension](http://refine.deri.ie/)
を導入することにより、RDFデータへの変換、エクスポートが行えます。


[Open Refine](http://openrefine.org/)
+
[GRefine RDF Extension](http://refine.deri.ie/)
では、マッピングツールを使うことにより表形式では表現できないRDFモデルを作成することができます。


また、半自動で
[DBpedia](http://ja.dbpedia.org/)
（Wikipedia）など外部のデータとリンクさせることができる、Linked Data化支援機能「Reconciliation」も備わっています。


[Open Refine](http://openrefine.org/)
と
[GRefine RDF Extension](http://refine.deri.ie/)
は、事前にPCにインストールしておく必要があります。<br />
インストール方法と、使い方、「Reconciliation」機能については、以下の資料を参考にしてください。

#### LOD連続講義 第5回「LODの作り方・使い方」

{{< slideshare id="36502563" >}}

 [1]: http://linkdata.org/home
 [2]: http://openrefine.org/
 [3]: http://refine.deri.ie/
 [4]: http://linkdata.org/tutorial