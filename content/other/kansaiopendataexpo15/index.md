---
title: 関西オープンデータEXPO’15～ハンズオンB～
author: webmaster
type: page
date: 2015-02-10T10:01:11+00:00
---

## 体験！Linked Open Data 〜オープンデータを作成・公開・活用してみよう〜

### タイムテーブル

| 時間 | 内容 |
|:-----------:|:--------------------------------------------------------------------------------------------------------------------------------------------- |
| 14:00-14:30 | LODの公開に関する講演<br>国立情報学研究所 准教授／Linked Open Data Initiative 副理事長<br>大向 一輝 氏 |
| 14:30-14:50 | オープンデータ/LOD公開の実践に関するライトニングトーク<br>(1) 自治体のオープンデータ導入事例の紹介<br>(2) WordPressのJSON-LDプラグイン「WordPress Make JSON-LD Plugin」の紹介<br>(3) LODお手軽アプリ作成ツールの紹介 |
| 14:50-15:45 | ハンズオン～オープンデータ/LODの可視化～|
| 15:45-16:00 | オープンデータの可視化ツールの紹介|

### 14:00～ LODの公開に関する講演

#### Linked Open Data入門 ～その意義と考え方～

国立情報学研究所 大向先生の講演資料です。

{{< slideshare id="44527397" >}}
  
### 14:30～ オープンデータ/LOD公開の実践に関するライトニングトーク

#### (2) WordPressのJSON-LDプラグイン「WordPress Make JSON-LD Plugin」の紹介

WordPress Make JSON-LD Plugin

<http://hideokamoto.github.io/make-json-ld/>

カスタムフィールドのデータをJSON-LD形式で出力するプラグインです。<br /> カスタムフィールド名を「schema:name」のような形式にすることで、簡単にJSON-LD化されたデータをみることができます。

#### (3) LODお手軽アプリ作成ツールの紹介

{{< slideshare id="44486781" >}}

### 14:50～ ハンズオン -オープンデータ/LODの可視化-


ハンズオンBでは、参加者の方々に
[LinkData](http://linkdata.org/)
を使ってクイズデータを、
[SlickQuiz-SPARQL](https://github.com/uedayou/SlickQuiz-SPARQL)
を使ってクイズアプリの作成を体験していただきました。


#### クイズデータ

[Googleスプレッドシート](https://docs.google.com/spreadsheets/d/17YVxdUFCJuL98MolG383v2SBjcxAtSsNsWrDSFTdrI8/edit?usp=sharing)
※ 現在、閲覧のみ可、編集は不可になっています。

[RDFデータ(LinkData.org)](http://linkdata.org/work/rdf1s2680i)

#### クイズアプリ

ハンズオンBの成果物です。

[関西オープンデータEXPO&#8217;15ハンズオンBで作成したクイズアプリ](http://lodc.jp/expo15quiz/)

[![クイズアプリ](/wp-content/uploads/2015/02/expo15quiz.jpg)](http://lodc.jp/expo15quiz/)

#### 解説サイト

- [SPARQLでマッシュアップ-LOD活用のための技術紹介-](http://uedayou.net/sparql-mashup/)
- [LODを検索する](/tool/searchdata/)

#### お手軽ビジュアライズ・アプリ作成ツール


アプリ | URL
--- | ---
Leaflet Simple SPARQL | [GitHub](https://github.com/uedayou/leaflet-simple-sparql)<br>[デモ](http://uedayou.net/lodchallenge/map-sample-osaka-city/)
SlickQuiz-SPARQL | [GitHub](https://github.com/uedayou/SlickQuiz-SPARQL)<br>[デモ](http://uedayou.net/SlickQuiz-SPARQL/)
FullCalendar SPARQL | [GitHub](https://github.com/uedayou/fullcalendar-sparql-js)<br>[デモ](http://uedayou.net/fullcalendar-linkdata-js/)
SPARQL Timeliner | [サイト](http://uedayou.net/SPARQLTimeliner/)<br>[GitHub](https://github.com/uedayou/SPARQLTimeliner)<br>[デモ](http://uedayou.net/osakabridge/)
○○危険地帯 | [GitHub](https://github.com/uedayou/dangerzone-sparql)</a><br>[デモ](http://uedayou.github.io/dangerzone-sparql/)<br>[Tips](http://qiita.com/uedayou/private/d4a26a9ac7db5fd82471)
BookSearch SPARQL js | [GitHub](https://github.com/uedayou/dangerzone-sparql)</a><br>[デモ](http://uedayou.github.io/dangerzone-sparql/)
sgvizler | [公式サイト](http://dev.data2000.no/sgvizler/)<br>[雛形HTML](http://uedayou.net/sparql-mashup/sgvizler/sgvizler-sample.html)<br />[デモ円グラフ](http://uedayou.net/sparql-mashup/sgvizler/kyoto-category-ranking.html)<br>[デモ棒グラフ](http://uedayou.net/sparql-mashup/sgvizler/kyoto-recommend-ranking.html)<br>[デモ無指向グラフ](http://uedayou.net/sparql-mashup/sgvizler/lodc-network.html)