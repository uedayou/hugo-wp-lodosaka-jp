---
title: LODを検索する
author: webmaster
type: page
date: 2015-01-20T00:46:57+00:00
---

Linked Open Data(LOD)で公開するサイトには、データをRDFデータベース(RDFストア)に格納して検索機能も併せて提供しているところがあります。  
RDFストアでLODを検索するには[SPARQL][1]というクエリ言語を使います。

[SPARQL][1]を使うことにより、自分の必要なデータのみを動的に抽出することができ、CSVやXML、JSONなどさまざまなフォーマットで出力することもできます。

<br />

### [SPARQL][1]で検索できるサイト

2020年11月現在の主に日本語コンテンツがあるSPARQLエンドポイントリストを以下で公開しています。

- 利用可能なSPARQLエンドポイントリスト(2020年8月版)

<https://qiita.com/uedayou/items/9e4c6029a2cb6b76de9f>

<br />

2015年時点でSPARQLで検索できるLOD提供サイトには例えば以下のようなものがあります。<br />
※ 2021年現在利用できないものも含まれます。


| サイト                                                              | 備考                       |
|:---------------------------------------------------------------- |:------------------------ |
| [LODチャレンジ<br />SPARQLエンドポイント(試行版)][2]                               | LODチャレンジデータセット部門応募作品のデータ |
| [DBPedia][3]                                                     | Wikipediaのデータ            |
| [DBPedia Japanese][4]                                            | Wikipedia日本語版のデータ        |
| [データシティ鯖江][5]                                                    | 福井県鯖江市のオープンデータ           |
| [Open Data METI][6]                                              | 経済産業省の統計データ              |
| [都道府県・市区町村コード情報][7]                                              |                          |
| [ヨコハマ・アート・LOD][8]                                                | 横浜に関するアーティスト情報、イベント情報    |
| [Europeana][9]                                                   | EUの美術館・博物館のデータ           |
| [LODAC Museum][10]                                               | 日本国内の美術館・博物館データ          |
| [The British Museum][11]                                         | 大英博物館のデータ                |
| [The British National Bibliography][12]                          | 大英図書館の書誌データ              |
| [Web NDL Authorities][13]                                        | 国立国会図書館の典拠データ            |
| [京都国際マンガミュージアム書誌情報LOD][14]                                       | マンガに関するデータ               |
| [i-Scover SPARQL Endpoint][15]                                   | 論文データ                    |
| [Linked Geo Data][16]                                            | 地理データ                    |
| [LODAC Location][10]                                             | 地理データ                    |
| [GeoNLP][17]                                                     | 地理データ                    |
| [気象庁XML用API][18]                                                 | 気象データ                    |
| [LODAC Species][19]                                              | 生物種データ                   |
| [日本語WordNet SPARQL endpoint][20]                                 | WordNetのデータ              |
| [IPADIC SPARQL endpoint][21]                                     | IPDICデータ                 |
| [東日本大震災アーカイブ Fukushima<br />SPARQLエンドポイント(テスト版)][22]                | 東日本大震災アーカイブデータ           |
| [XMRL Linked Open Data][23]                                      | 金融庁EDINETのデータ            |
| [LinkedBrainz<br />SPARQL Query Examples over MusicBrainz Data][24] | CDシングル、アルバム、アーティストデータ    |
| [Linked Open Vocabularies][25]                                   | 語彙のデータ                   |

<br />

### [SparqlEPCU][26]:LOD作成・活用支援サイト

[SparqlEPCU][26]を使えば、自分で作成したLODを使って[SPARQL][1]を検索できるWeb API(SPARQLエンドポイント)を簡単に作ることができます。

SparqlEPCU については、以下の資料をご覧ください。

{{< slideshare id="39222604" >}}

### [SPARQL](http://www.asahi-net.or.jp/~ax2s-kmtn/internet/rdf/REC-sparql11-query-20130321.html)の書き方

SPARQLの書き方は、以下のサイトとスライドで詳しく紹介されています。

- SPARQLでマッシュアップ- LOD活用のための技術紹介-
<http://uedayou.net/sparql-mashup/#query>

{{< slideshare id="42432459" >}}


 [1]: http://www.asahi-net.or.jp/~ax2s-kmtn/internet/rdf/REC-sparql11-query-20130321.html
 [2]: http://lodc.jp
 [3]: http://dbpedia.org/sparql
 [4]: http://ja.dbpedia.org/sparql
 [5]: http://sparql.odp.jig.jp/sparql.html
 [6]: http://datameti.go.jp/sparql
 [7]: http://statdb.nstac.go.jp/lod/sparql
 [8]: http://archive.yafjp.org/test/inspection.php
 [9]: http://europeana.ontotext.com/sparql
 [10]: http://lod.ac/sparql
 [11]: http://collection.britishmuseum.org/sparql
 [12]: http://bnb.data.bl.uk/flint-sparql
 [13]: http://id.ndl.go.jp/auth/ndla?query=
 [14]: http://mdlab.slis.tsukuba.ac.jp/lodc2012/kmm/
 [15]: http://monticola.lodac.nii.ac.jp/sparql
 [16]: http://linkedgeodata.org/sparql
 [17]: http://geolod.ex.nii.ac.jp/snorql/
 [18]: http://api.aitc.jp/ds/
 [19]: http://lod.ac/species/sparql
 [20]: http://wordnet.jp/repositories/wordnet-ja#query/d/select%20?s%20?p%20?o%20%7B?s%20?p%20?o%7D
 [21]: http://ipadic.jp:10035/repositories/ipadic#query/d/select%20?s%20?p%20?o%20%7B?s%20?p%20?o%7D
 [22]: http://fukushima.archive-disasters.jp/sparqlendpoint/
 [23]: http://www.xbrl-lod.org/query/
 [24]: http://linkedbrainz.org/sparql
 [25]: http://lov.okfn.org/dataset/lov/sparql
 [26]: http://lodcu.cs.chubu.ac.jp/SparqlEPCU/