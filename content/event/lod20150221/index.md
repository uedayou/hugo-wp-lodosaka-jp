---
title: 第5回Linked Open Dataハッカソン関西 in インターナショナルオープンデータデイ大阪
author: webmaster
type: page
date: 2015-02-20T03:48:30+00:00
---

第5回Linked Open Dataハッカソン関西 は、昨年に引き続き「[インターナショナルオープンデータデイ2015][1]」の大阪会場としてハッカソン、データソンを開催しました。

{{< figure src="/wp-content/uploads/2015/02/bnr_odd2015.png" alt="" width="240">}}

{{< figure src="/wp-content/uploads/2015/02/img_5681.jpg" alt="" width="426">}}

### 日時：

2015年2月21日（土）  

### 会場：

[大阪イノベーションハブ](http://www.innovation-osaka.jp/ja/)  

### イベント申込サイト：

<http://www.innovation-osaka.jp/ja/events/4679>  

### プログラム：

[第5回Linked Open Dataハッカソン関西 in インターナショナルオープンデータデイ大阪(2/21)開催](/news/%E7%AC%AC5%E5%9B%9Elod%E3%83%8F%E3%83%83%E3%82%AB%E3%82%BD%E3%83%B3%E9%96%A2%E8%A5%BFin%E3%82%AA%E3%83%BC%E3%83%97%E3%83%B3%E3%83%87%E3%83%BC%E3%82%BF%E3%83%87%E3%82%A4%E9%96%8B%E5%82%AC/)  

## 会場の様子

{{< figure src="/wp-content/uploads/2015/02/iodd_photo02.jpg" alt="" width="90%">}}
  
## 講演1

京都大学 亀田先生に、Linked Open Data の仕組みと重要性について講演していただきました。

### タイトル

Webアーキテクチャーとしてのオープンデータ -LOD, RDF、五つ星データの本当の意味-  

### 講演者

京都大学 地域研究統合情報センター [亀田 尭宙](http://www.cias.kyoto-u.ac.jp/staff/kameda.php)氏  

{{< slideshare id="44948958" >}}  

## 講演2

「Osaka (& Kansai) おもろい事例？？連発」と題して、これまで大阪や関西で行われたハッカソン等で開発されたオープンデータを活用するおもろい事例を紹介しました。

### タイトル

Osaka （＆Kansai）おもろい事例？？連発  

### 講演者

LODチャレンジ実行委員会 関西支部長／大阪大学 古崎 晃司 氏  

{{< slideshare id="44939647" >}}  

## RDF変換ツールの使い方

CSV形式を簡単にRDFデータに変換できるツールを紹介しました。  

### CSV2RDF

[ダウンロード先](http://lodosaka.jp/tool/csv2rdf20150221.zip)  


このツールの利用には、[Java Runtime Environment(JRE)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)が必要です。事前にダウンロードしてください。
上記のダウンロード先から、Zipファイルをダウンロードし、適当なフォルダに解凍してください。  

## ハッカソン・データソン 成果

午後からは、チームに分かれてハッカソンやデータソンを行っていただきました。
イベント中には、LODの技術を利用したたくさんの成果が誕生しました。  

### Pathway解析のためのSPARQL wrapper packageの作成

{{< slideshare id="44954335" >}}  

#### PIEROutil

[ソースコード](https://github.com/kozo2/PIEROutil)  

### Jogging Course Info

[![Jogging Course Info](/wp-content/uploads/2015/02/iodd2015_app_jogging_cource_info.jpg)](http://mmasuda.github.io/GreenCorridor/index.html)  

#### デモアプリ

<http://mmasuda.github.io/GreenCorridor/index.html>  

#### データ

<http://data.lodosaka.jp/GreenCorridor.ttl>  

### 高槻市インターネット歴史館 by チーム高槻

[![高槻市インターネット歴史館 by チーム高槻](/wp-content/uploads/2015/02/iodd2015_app_takatsuki_history_map.jpg)](http://lodc.jp/takatsukihistorymap/)  

#### アプリ

<http://lodc.jp/takatsukihistorymap/>  


#### データ(SPARQLエンドポイント)

<http://lodcu.cs.chubu.ac.jp/SparqlEPCU/api/takatsuki_rekishikan>  


### スイスイちゃりマップ

[![スイスイちゃりマップ](/wp-content/uploads/2015/02/iodd2015_app_suichari.jpg)](http://suichari.lodosaka.jp/)  

#### 紹介ページ

<http://suichari.lodosaka.jp/index.html>  

#### デモアプリ

<http://suichari.lodosaka.jp/apps/>  

### プラネタリウムなび を 5つ星オープンデータ に

プラネタリウム横断検索サイト「プラネタリウムなび」のRDFデータが、ハッカソン中に
[5つ星オープンデータ](http://5stardata.info/ja/)
になりました。  

#### プラネタリウムなび

[![プラネタリウムなび](/wp-content/uploads/2015/02/iodd2015_app_planetarium_navi.jpg)](http://museums-info.net/planetarium/navi/)  

たとえば、「<http://www.museums-info.net/resource/>」+「プラネタリウム名」でブラウザにアクセスすると、以下のようにプラネタリウムのRDFデータを見ることができます。  

![](/wp-content/uploads/2015/02/iodd2015_data_planetarium_lod.jpg)  

<http://www.museums-info.net/resource/大阪市立科学館>をブラウザで開いたときの例  


### なんでもリンク

テキストフォームに適当な文字列を入力すると、その文字列を含むデータのURIをDBpediaなどから探してきてくれるツールです。  

[5つ星オープンデータ](http://5stardata.info/ja/) に対応するにはとても便利なツールです。  

[![なんでもリンク](/wp-content/uploads/2015/02/iodd2015_app_nandemo_link.jpg)](http://link.lodosaka.jp/)  

#### アプリ

<http://link.lodosaka.jp/>  

#### ソースコード

<https://github.com/yayamamo/anyLink>  



[1]: http://odd15.okfn.jp/