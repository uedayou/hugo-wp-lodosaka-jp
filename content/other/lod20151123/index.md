---
title: 関西オープンデータデイ
author: webmaster
type: page
date: 2015-11-23T02:16:34+09:00
---

2015年11月23日、グランフロント大阪 大阪イノベーションハブで「関西オープンデータディ ー検索したおしたんディー」を開催しています。

![関西オープンデータデイ](/wp-content/uploads/2015/11/safe_image.jpg)

## 日時：

2015年11月23日（土）

## 会場：

[大阪イノベーションハブ](http://www.innovation-osaka.jp/ja/)

## イベント用FBページ：

<https://www.facebook.com/events/519662078184283/> 

## 資料、ツール、検索API等

[参加者向け情報共有用スプレッドシート][1]  
※ 最新の情報はこちらをご覧ください。

### SPARQL エンドポイント

#### DBpediaJapaneseとの統合検索用+DBpedia日本語版

<http://lod.hozo.jp/repositories/kod>
※ チュートリアルで利用します。

#### LODチャレンジデー神戸の成果

<http://lod.hozo.jp/repositories/lodosaka>

#### 格納されているデータ一覧

**PREFIX**

    prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    prefix cc:   <http://creativecommons.org/ns#>
    prefix xsd:  <http://www.w3.org/2001/XMLSchema#>
    prefix rss:  <http://purl.org/rss/2.0/>
    prefix geo:  <http://www.w3.org/2003/01/geo/wgs84_pos#>
    prefix schema: <http://schema.org/>
    prefix ldo:  <http://data.lodosaka.jp/property#>
    prefix ic: <http://imi.ipa.go.jp/ns/core/rdf#>

**(1) DBPedia日本語**

グラフURI： `<http://ja.dbpedia.org/>`

**(2) 大阪市の施設情報**  

グラフURI： `<http://data.lodosaka.jp/kod/osaka/mapnavoskdat_shisetsuall>`

| プロパティ名            |   データ型    |   元データの項目名    |
|:----------------- |:---------:|:-------------:|
| geo:long          | xsd:float |       X       |
| geo:lat           | xsd:float |       Y       |
| rdfs:label        |    ja     |      施設名      |
| ldo:dbp-ja-link   |           | ※DBpediaへのリンク |
| ldo:施設名かな         |    ja     |     施設名かな     |
| ldo:施設名<br />（施設名かな） |    ja     | 施設名<br />（施設名かな） |
| ic:住所             |    ja     |      所在地      |
| ic:市町村            |    ja     |     ※市町村      |
| ic:区              |    ja     |      地区名      |
| ic:電話番号           |           |      TEL      |
| ic:FAX番号          |           |      FAX      |
| ldo:詳細情報          |    ja     |     詳細情報      |
| ic:利用可能時間         |    ja     |     開館時間      |
| ic:Webサイト         |           |      URL      |
| ldo:バリアフリー情報      | xsd:float |   バリアフリー情報    |
| ldo:駐輪場_PC        | xsd:float |    駐輪場 PC     |
| ldo:駐輪場_携         |    ja     |     駐輪場 携     |
| ldo:大分類           |    ja     |      大分類      |
| ic:種別             |    ja     |      小分類      |
| ldo:カテゴリ          |           |     カテゴリ      |
| ldo:アイコン番号        |           |    アイコン番号     |
| ldo:施設ID          |           |     施設ID      |

<br />

**(3) 和歌山県の公共施設** 

グラフURI： `<http://data.lodosaka.jp/kod/wakayama/list-of-public-facilities/>`

| プロパティ名              | データ型 |    元データの項目名     |
|:------------------- |:----:|:---------------:|
| rdfs:label          |  ja  |       名称        |
| ldo:dbp-ja-link     |      |  ※DBpediaへのリンク  |
| ic:住所               |  ja  |       住所        |
| ldo:分類              |      |       分類        |
| ic:都道府県             |  ja  |       住所1       |
| ic:市町村              |  ja  |       住所2       |
| ldo:住所3             |  ja  |       住所3       |
| ic:電話番号             |      |       電話        |
| ic:FAX番号            |      |       FAX       |
| ic:利用可能時間           |  ja  |      利用時間       |
| ldo:階数              |  ja  |       階数        |
| ldo:定休日             |  ja  |       定休日       |
| ic:駐車場              |  ja  |       駐車場       |
| ldo:敷地内の状況<br />及び施設入口 |  ja  | 敷地内の状況<br />及び施設入口 |
| ldo:誘導施設            |  ja  |      誘導施設       |
| ldo:案内設備            |  ja  |      案内設備       |
| ldo:昇降設備            |  ja  |      昇降設備       |
| ldo:トイレ             |  ja  |       トイレ       |
| ldo:公衆電話            |  ja  |      公衆電話       |
| ldo:その他の設備          |  ja  |     その他の設備      |
| ic:備考               |  ja  |       備考        |
| ic:種別               |  ja  |      カテゴリー      |

<br />

**(4) 大阪市のRSS（PUSH大阪用データ）**

グラフURI： `<http://lodosaka.jp/osakarss>`

| プロパティ名                           |     データ型     |         元データの項目名          |
|:-------------------------------- |:------------:|:-------------------------:|
| ldo:area_label                   |     リテラル     | 大阪市 or 各区<br />（例：北区，都島区．．．） |
| ldo:category                     |     リテラル     |           カテゴリ            |
| ldo:category_label               |      ja      |           カテゴリ名           |
| rss:title                        |      ja      |           タイトル            |
| rss:link                         |              |          記事のURL           |
| ldo:keywords &#8220;all&#8221; ; |              | |
| ldo:keywords_label               |     リテラル     |           キーワード           |
| ldo:lastUpDate                   | xsd:dateTime |            更新日            |
| rss:pubDate                      | xsd:dateTime |            公開日            |

<br />

**(5) 高槻市の「赤ちゃんの駅」**

グラフURI： `<http://data.lodosaka.jp/kod/takatsuki/takatsuki_city_babyst>`

| プロパティ名          |   データ型    |   元データの項目名    |
|:--------------- |:---------:|:-------------:|
| rdfs:label      |    ja     |      名前       |
| ldo:dbp-ja-link |           | ※DBpediaへのリンク |
| ic:住所           |    ja     |      住所       |
| ic:市町村          |    ja     |     ※市町村      |
| ic:電話番号         |           |     電話番号      |
| ic:FAX番号        |           |      FAX      |
| geo:lat         | xsd:float |      経度       |
| geo:long        | xsd:float |      緯度       |
| ic:Webサイト       |           |  WebサイトのURL   |

詳しくは[こちら][2]をご覧ください。

 [1]: https://docs.google.com/spreadsheets/d/1-3DaszoByJSwBKP7rnaKTcru8tohQoV6y9KXDuuCcmc/edit?pli=1#gid=0
 [2]: https://docs.google.com/spreadsheets/d/1cmNJxYGqmyWGIu2IMHK_UTGdk83_YPlM3WtsYbW6xqc/edit#gid=66768040