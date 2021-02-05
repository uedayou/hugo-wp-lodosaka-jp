---
title: SPARQLクエリ集
author: webmaster
type: page
date: 2015-10-19T03:29:32+00:00
---

## 基本的なSPARQLクエリ

### すべてトリプルを取得

    select *
    where { 
      ?s ?p ?o . 
    }
    LIMIT 100
    

[検索例(DBpedia日本語版)][1]

### 「東京都を主語（Subject）に含む」トリプルの述語(?p）と目的語(?o)を取得する

    select distinct ?p ?o
    where { 
      <http://ja.dbpedia.org/resource/東京都> ?p ?o . 
    }
    LIMIT 100
    

[検索例(DBpedia日本語版)][2]

### 「ラベルに“大阪”を含む」トリプルの主語(?s)

    select distinct ?s where {
      ?s <http://www.w3.org/2000/01/rdf-schema#label>? "大阪"@ja .
    }LIMIT 100
    

[検索例(DBpedia日本語版)][3]

### 「ラベルが“大阪”と一致する」トリプルの主語(?s)につながっている述語(?p)と目的語(?o)

    select distinct ?s where {
      ?s <http://www.w3.org/2000/01/rdf-schema#label> ?o 
      FILTER(regex(str(?o), "大阪" )) .
    }LIMIT 100
    

[検索例(DBpedia日本語版)][4]

### PREFIXの利用

    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    select distinct ?p ?o where {
      ?s rdfs:label "大阪"@ja . 
    }LIMIT 100
    

[検索例(DBpedia日本語版)][5]

### OFFSETの利用

    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    select distinct ?p ?o
    where { 
       dbpedia-ja:東京都 ?p ?o . 
    }
    LIMIT 10
    OFFSET 10
    

[検索例(DBpedia日本語版)][6]

### 主語が同じ時の省略表現

    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    select distinct ?p ?o where {
      ?s rdfs:label "大阪"@ja ;  
         ?p ?o.
    }LIMIT 100
    

[検索例(DBpedia日本語版)][7]

## いろいろな組み合わせを試す(DBpedia日本語版編)

### 大阪府を主語とするトリプル一覧

    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    select distinct * where {
      dbpedia-ja:大阪府 ?p ?o.
    }
    

[検索例(DBpedia日本語版)][8]

### 大阪府が持つプロパティ一覧

    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    select distinct ?p where {
      dbpedia-ja:大阪府 ?p ?o.
    }
    

[検索例(DBpedia日本語版)][9]

### 大阪府の隣接都道府県

    PREFIX prop-ja: <http://ja.dbpedia.org/property/>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    
    select distinct * where {
      dbpedia-ja:大阪府  prop-ja:隣接都道府県 ?o.
    }
    

[検索例(DBpedia日本語版)][10]

### すべての隣接都道府県の組

    PREFIX prop-ja: <http://ja.dbpedia.org/property/>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    
    select distinct * where {
      ?s  prop-ja:隣接都道府県 ?o.
    }
    

[検索例(DBpedia日本語版)][11]

### 大阪府の隣接都道府県の数

    PREFIX prop-ja: <http://ja.dbpedia.org/property/>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    
    select distinct count(?o) where {
      dbpedia-ja:大阪府  prop-ja:隣接都道府県 ?o.
    }
    

[検索例(DBpedia日本語版)][12]

### 大阪府の隣接都道府県の数(結果を変数に代入)

    PREFIX prop-ja: <http://ja.dbpedia.org/property/>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    
    select distinct count(?o) AS ?count where {
      dbpedia-ja:大阪府  prop-ja:隣接都道府県 ?o.
    }
    

[検索例(DBpedia日本語版)][13]

### 不要なプロパティをFILTERで除外

    PREFIX prop-ja: <http://ja.dbpedia.org/property/>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    
    select distinct * where {
      dbpedia-ja:大阪府  ?p ?o.
      FILTER(?p != dbpedia-owl:wikiPageWikiLink) .
    }
    

[検索例(DBpedia日本語版)][14]

### タイプ一覧の取得

    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    
    select distinct ?o where {
      ?s rdf:type ?o.
    }LIMIT 100
    

[検索例(DBpedia日本語版)][15]

### 都道府県の一覧を取得

    PREFIX dbpedia-owl:  <http://dbpedia.org/ontology/>
    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    
    select distinct ?s where {
      ?s rdf:type dbpedia-owl:Place.
      ?s dbpedia-owl:wikiPageWikiLink category-ja:日本の都道府県.
    }
    

[検索例(DBpedia日本語版)][15]

### 郵便番号でソート（昇順）

    PREFIX dbpedia-owl:  <http://dbpedia.org/ontology/>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    
    select distinct ?s ?o where {
      ?s rdf:type dbpedia-owl:Place;
         dbpedia-owl:wikiPageWikiLink category-ja:日本の都道府県;
         dbpedia-owl:postalCode?? ?o.        
    
    }ORDER BY ?o
    

[検索例(DBpedia日本語版)][16]

### 郵便番号でソート（降順）

    PREFIX dbpedia-owl:  <http://dbpedia.org/ontology/>
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    
    select distinct ?s ?o where {
      ?s rdf:type dbpedia-owl:Place;
         dbpedia-owl:wikiPageWikiLink category-ja:日本の都道府県;
         dbpedia-owl:postalCode ?o.        
    
    }ORDER BY DESC(?o)
    

[検索例(DBpedia日本語版)][17]

### 日本の都道府県を「隣接自治体の数」でソート

    PREFIX dbpedia-owl:  <http://dbpedia.org/ontology/>
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    
    select distinct ?s count(?o) AS ?c where {
      ?s rdf:type dbpedia-owl:Place;
         dbpedia-owl:wikiPageWikiLink category-ja:日本の都道府県;
         prop-ja:隣接都道府県 ?o.  
    }ORDER BY ?c
    

[検索例(DBpedia日本語版)][18]

### 各都道府県で生まれた政治家

    PREFIX dbpedia-owl:  <http://dbpedia.org/ontology/>
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    
    select distinct ?pref  ?s where {
      ?pref rdf:type dbpedia-owl:Place.
      ?pref dbpedia-owl:wikiPageWikiLink category-ja:日本の都道府県.
      ?s rdf:type dbpedia-owl:Politician;
          dbpedia-owl:birthPlace ?pref.
    }ORDER BY ?pref
    

[検索例(DBpedia日本語版)][19]

### 各都道府県で生まれた政治家の数

    PREFIX dbpedia-owl:  <http://dbpedia.org/ontology/>
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    
    select distinct ?pref (count(?s) AS ?c) where {
      ?pref rdf:type dbpedia-owl:Place.
      ?pref dbpedia-owl:wikiPageWikiLink category-ja:日本の都道府県.
      ?s rdf:type dbpedia-owl:Politician;
          dbpedia-owl:birthPlace ?pref.
    }GROUP BY ?pref
    ORDER BY ?c
    

[検索例(DBpedia日本語版)][20]

### 「出生地が大阪府」または「出生地が東京都」の政治家

    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX dbpedia-owl:  <http://dbpedia.org/ontology/>    
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    
    select distinct ?s ?pref where {
      {?s rdf:type dbpedia-owl:Politician;
          dbpedia-owl:birthPlace dbpedia-ja:大阪府.}
      UNION{?s rdf:type dbpedia-owl:Politician;
          dbpedia-owl:birthPlace dbpedia-ja:東京都.}
      ?s dbpedia-owl:birthPlace ?pref.
    }ORDER BY ?pref
    

[検索例(DBpedia日本語版)][21]

## [第36回SWO研究会][22]のハンズオン成果

### 都道府県ごとの、日本のアイドルの人数

    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX dbpedia-owl:  <http://dbpedia.org/ontology/>
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    
    select distinct ?pref (count(?s) AS ?c) where {
      ?pref rdf:type dbpedia-owl:Place.
      ?pref dbpedia-owl:wikiPageWikiLink category-ja:日本の都道府県.
      ?s rdf:type dbpedia-owl:Person;
          dbpedia-owl:wikiPageWikiLink category-ja:日本のアイドル;
          dbpedia-owl:birthPlace ?pref.
    }GROUP BY ?pref
    ORDER BY ?c
    

[検索例(DBpedia日本語版)][23]

### ウィキペディアに掲載された日本人(nationalityがJapan)の生誕年ごとの人数集計

    PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>
    PREFIX dbpedia-ja: <http://ja.dbpedia.org/resource/>
    
    SELECT ?year COUNT(?s) WHERE {
    ?s dbpedia-owl:nationality dbpedia-ja:Japan ;
    dbpedia-owl:birthDate ?date.
    }
    GROUP BY (year(?date) AS ?year)
    ORDER BY ?year
    

[検索例(DBpedia日本語版)][24]

### 生誕年の新しい順

昔の人が2020年生まれになっている

    select distinct ?s ?date where { 
    ?s dbpedia-owl:birthDate ?date.
    }
    ORDER BY desc(year(?date))
    LIMIT 100
    

[検索例(DBpedia日本語版)][25]

### 日本百名山の標高順

    select *
    where 
    {
      ?uri dbpedia-owl:wikiPageWikiLink category-ja:日本百名山.
      ?uri rdf:type schema:Mountain.
      ?uri foaf:name ?name.
      ?uri foaf:depiction ?image.
      ?uri prop-ja:標高 ?altitude.
    }
    order by ?altitude
    

[検索例(DBpedia日本語版)][26]

### 戦国時代・安土桃山時代の戦に参加した武将(回数順)

    PREFIX category-ja: <http://ja.dbpedia.org/resource/Category:>
    SELECT DISTINCT ?person count(?war) AS ?c WHERE {
    {?war dbpedia-owl:wikiPageWikiLink category-ja:日本の戦国時代の戦い}
    UNION
    {?war dbpedia-owl:wikiPageWikiLink category-ja:安土桃山時代の戦い}
    ?war dbpedia-owl:opponents ?person .
    }
    GROUP BY ?person
    ORDER BY DESC(?c)
    

[検索例(DBpedia日本語版)][27]

### 「学会」を含む組織の創設年度順列挙

産総研 西村さん作

国立国会図書館典拠データ検索・提供サービスで利用可能なクエリ  
<http://id.ndl.go.jp/auth/ndla/?query=>

    select distinct * where{
      ?id <http://xmlns.com/foaf/0.1/name> ?name.
      ?id a <http://xmlns.com/foaf/0.1/Organization>;
      <http://RDVocab.info/ElementsGr2/dateOfEstablishment> ?date;
      <http://RDVocab.info/ElementsGr2/corporateHistory> ?history.
      filter (regex(str(?name), "学会"))
    }
    order by ?date
    

[Web NDL Authoritiesでの例][28]

[SPARQLチュートリアル＠第36回SWO研究会-DBpediaシンポジウム][29] より引用

## その他のSPARQLクエリ集

  * [LODAC Wiki SPARQLスニペット][30]
  * [Wikibase/Indexing/SPARQL Query Examples][31]
  * [Qiita：SPARQLに関する投稿][32]
  * [Gist：Search “SPARQL”][33]

 [1]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=select+*%0D%0Awhere+%7B+%0D%0A++%3Fs+%3Fp+%3Fo+.+%0D%0A%7D%0D%0ALIMIT+100&format=text%2Fhtml&timeout=0&debug=on
 [2]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=select+distinct+%3Fp+%3Fo%0D%0Awhere+%7B+%0D%0A++%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%E6%9D%B1%E4%BA%AC%E9%83%BD%3E+%3Fp+%3Fo+.+%0D%0A%7D%0D%0ALIMIT+100&format=text%2Fhtml&timeout=0&debug=on
 [3]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=select+distinct+%3Fs+where+%7B%0D%0A++%3Fs+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23label%3E++%22%E5%A4%A7%E9%98%AA%22%40ja+.%0D%0A%7DLIMIT+100&format=text%2Fhtml&timeout=0&debug=on
 [4]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=select+distinct+%3Fs+where+%7B%0D%0A++%3Fs+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23label%3E+%3Fo+%0D%0A++FILTER%28regex%28str%28%3Fo%29%2C+%22%E5%A4%A7%E9%98%AA%22+%29%29+.%0D%0A%7DLIMIT+100&format=text%2Fhtml&timeout=0&debug=on
 [5]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0Aselect+distinct+%3Fp+%3Fo+where+%7B%0D%0A++%3Fs+rdfs%3Alabel+%22%E5%A4%A7%E9%98%AA%22%40ja+.++%0D%0A++%3Fs+%3Fp+%3Fo.%0D%0A%7DLIMIT+100&format=text%2Fhtml&timeout=0&debug=on
 [6]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0Aselect+distinct+%3Fp+%3Fo%0D%0Awhere+%7B+%0D%0A+++dbpedia-ja%3A%E6%9D%B1%E4%BA%AC%E9%83%BD+%3Fp+%3Fo+.+%0D%0A%7D%0D%0ALIMIT+10%0D%0AOFFSET+10&format=text%2Fhtml&timeout=0&debug=on
 [7]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0Aselect+distinct+%3Fp+%3Fo+where+%7B%0D%0A++%3Fs+rdfs%3Alabel+%22%E5%A4%A7%E9%98%AA%22%40ja+%3B++%0D%0A+++++%3Fp+%3Fo.%0D%0A%7DLIMIT+100&format=text%2Fhtml&timeout=0&debug=on
 [8]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0Aselect+distinct+*+where+%7B%0D%0A++dbpedia-ja%3A%E5%A4%A7%E9%98%AA%E5%BA%9C+%3Fp+%3Fo.%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on
 [9]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0Aselect+distinct+%3Fp+where+%7B%0D%0A++dbpedia-ja%3A%E5%A4%A7%E9%98%AA%E5%BA%9C+%3Fp+%3Fo.%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on
 [10]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+prop-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fproperty%2F%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0A%0D%0Aselect+distinct+*+where+%7B%0D%0A++dbpedia-ja%3A%E5%A4%A7%E9%98%AA%E5%BA%9C++prop-ja%3A%E9%9A%A3%E6%8E%A5%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C+%3Fo.%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on
 [11]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+prop-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fproperty%2F%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0A%0D%0Aselect+distinct+*+where+%7B%0D%0A++%3Fs++prop-ja%3A%E9%9A%A3%E6%8E%A5%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C+%3Fo.%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on
 [12]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+prop-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fproperty%2F%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0A%0D%0Aselect+distinct+count%28%3Fo%29+where+%7B%0D%0A++dbpedia-ja%3A%E5%A4%A7%E9%98%AA%E5%BA%9C++prop-ja%3A%E9%9A%A3%E6%8E%A5%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C+%3Fo.%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on
 [13]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+prop-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fproperty%2F%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0A%0D%0Aselect+distinct+count%28%3Fo%29+AS+%3Fcount+where+%7B%0D%0A++dbpedia-ja%3A%E5%A4%A7%E9%98%AA%E5%BA%9C++prop-ja%3A%E9%9A%A3%E6%8E%A5%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C+%3Fo.%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on
 [14]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+prop-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fproperty%2F%3E%0D%0A++++PREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0A%0D%0A++++select+distinct+*+where+%7B%0D%0A++++++dbpedia-ja%3A%E5%A4%A7%E9%98%AA%E5%BA%9C++%3Fp+%3Fo.%0D%0A++++++FILTER%28%3Fp+%21%3D+dbpedia-owl%3AwikiPageWikiLink%29+.%0D%0A++++%7D&format=text%2Fhtml&timeout=0&debug=on
 [15]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+dbpedia-owl%3A++%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0A++++%0D%0Aselect+distinct+%3Fs+where+%7B%0D%0A%3Fs+rdf%3Atype+dbpedia-owl%3APlace.%0D%0A%3Fs+dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C.%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on
 [16]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-owl%3A++%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0APREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0A%0D%0Aselect+distinct+%3Fs+%3Fo+where+%7B%0D%0A++%3Fs+rdf%3Atype+dbpedia-owl%3APlace%3B%0D%0A+++++dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C%3B%0D%0A+++++dbpedia-owl%3ApostalCode+++%3Fo.++++++++%0D%0A%0D%0A%7DORDER+BY+%3Fo&format=text%2Fhtml&timeout=0&debug=on
 [17]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-owl%3A++%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0APREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0A%0D%0Aselect+distinct+%3Fs+%3Fo+where+%7B%0D%0A++%3Fs+rdf%3Atype+dbpedia-owl%3APlace%3B%0D%0A+++++dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C%3B%0D%0A+++++dbpedia-owl%3ApostalCode+%3Fo.++++++++%0D%0A%0D%0A%7DORDER+BY+DESC%28%3Fo%29&format=text%2Fhtml&timeout=0&debug=on
 [18]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-owl%3A++%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0APREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0A%0D%0Aselect+distinct+%3Fs+count%28%3Fo%29+AS+%3Fc+where+%7B%0D%0A++%3Fs+rdf%3Atype+dbpedia-owl%3APlace%3B%0D%0A+++++dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C%3B%0D%0A+++++prop-ja%3A%E9%9A%A3%E6%8E%A5%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C+%3Fo.++%0D%0A%7DORDER+BY+%3Fc&format=text%2Fhtml&timeout=0&debug=on
 [19]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-owl%3A++%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0APREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0A%0D%0Aselect+distinct+%3Fpref++%3Fs+where+%7B%0D%0A++%3Fpref+rdf%3Atype+dbpedia-owl%3APlace.%0D%0A++%3Fpref+dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C.%0D%0A++%3Fs+rdf%3Atype+dbpedia-owl%3APolitician%3B%0D%0A++++++dbpedia-owl%3AbirthPlace+%3Fpref.%0D%0A%7DORDER+BY+%3Fpref&format=text%2Fhtml&timeout=0&debug=on
 [20]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-owl%3A++%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0APREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0A%0D%0Aselect+distinct+%3Fpref+%28count%28%3Fs%29+AS+%3Fc%29+where+%7B%0D%0A++%3Fpref+rdf%3Atype+dbpedia-owl%3APlace.%0D%0A++%3Fpref+dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C.%0D%0A++%3Fs+rdf%3Atype+dbpedia-owl%3APolitician%3B%0D%0A++++++dbpedia-owl%3AbirthPlace+%3Fpref.%0D%0A%7DGROUP+BY+%3Fpref%0D%0AORDER+BY+%3Fc&format=text%2Fhtml&timeout=0&debug=on
 [21]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-owl%3A++%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0APREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0A%0D%0Aselect+distinct+%3Fs+%3Fpref+where+%7B%0D%0A++%7B%3Fs+rdf%3Atype+dbpedia-owl%3APolitician%3B%0D%0A++++++dbpedia-owl%3AbirthPlace+dbpedia-ja%3A%E5%A4%A7%E9%98%AA%E5%BA%9C.%7D%0D%0A++UNION%7B%3Fs+rdf%3Atype+dbpedia-owl%3APolitician%3B%0D%0A++++++dbpedia-owl%3AbirthPlace+dbpedia-ja%3A%E6%9D%B1%E4%BA%AC%E9%83%BD.%7D%0D%0A++%3Fs+dbpedia-owl%3AbirthPlace+%3Fpref.%0D%0A%7DORDER+BY+%3Fpref&format=text%2Fhtml&timeout=0&debug=on
 [22]: https://sites.google.com/site/sigswo15/papers/36program
 [23]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbpedia-owl%3A++%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0APREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0A%0D%0Aselect+distinct+%3Fpref+%28count%28%3Fs%29+AS+%3Fc%29+where+%7B%0D%0A++%3Fpref+rdf%3Atype+dbpedia-owl%3APlace.%0D%0A++%3Fpref+dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E9%83%BD%E9%81%93%E5%BA%9C%E7%9C%8C.%0D%0A++%3Fs+rdf%3Atype+dbpedia-owl%3APerson%3B%0D%0A++++++dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E3%82%A2%E3%82%A4%E3%83%89%E3%83%AB%3B%0D%0A++++++dbpedia-owl%3AbirthPlace+%3Fpref.%0D%0A%7DGROUP+BY+%3Fpref%0D%0AORDER+BY+%3Fc&format=text%2Fhtml&timeout=0&debug=on
 [24]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+dbpedia-owl%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+dbpedia-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2F%3E%0D%0A%0D%0ASELECT+%3Fyear+COUNT%28%3Fs%29+WHERE+%7B%0D%0A%3Fs+dbpedia-owl%3Anationality+dbpedia-ja%3AJapan+%3B%0D%0Adbpedia-owl%3AbirthDate+%3Fdate.%0D%0A%7D%0D%0AGROUP+BY+%28year%28%3Fdate%29+AS+%3Fyear%29%0D%0AORDER+BY+%3Fyear&format=text%2Fhtml&timeout=0&debug=on
 [25]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=select+distinct+%3Fs+%3Fdate+where+%7B+%0D%0A%3Fs+dbpedia-owl%3AbirthDate+%3Fdate.%0D%0A%7D%0D%0AORDER+BY+desc%28year%28%3Fdate%29%29%0D%0ALIMIT+100&format=text%2Fhtml&timeout=0&debug=on
 [26]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=select+*%0D%0Awhere+%0D%0A%7B%0D%0A++%3Furi+dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E7%99%BE%E5%90%8D%E5%B1%B1.%0D%0A++%3Furi+rdf%3Atype+schema%3AMountain.%0D%0A++%3Furi+foaf%3Aname+%3Fname.%0D%0A++%3Furi+foaf%3Adepiction+%3Fimage.%0D%0A++%3Furi+prop-ja%3A%E6%A8%99%E9%AB%98+%3Faltitude.%0D%0A%7D%0D%0Aorder+by+%3Faltitude&format=text%2Fhtml&timeout=0&debug=on
 [27]: http://ja.dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fja.dbpedia.org&query=PREFIX+category-ja%3A+%3Chttp%3A%2F%2Fja.dbpedia.org%2Fresource%2FCategory%3A%3E%0D%0ASELECT+DISTINCT+%3Fperson+count%28%3Fwar%29+AS+%3Fc+WHERE+%7B%0D%0A%7B%3Fwar+dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E6%97%A5%E6%9C%AC%E3%81%AE%E6%88%A6%E5%9B%BD%E6%99%82%E4%BB%A3%E3%81%AE%E6%88%A6%E3%81%84%7D%0D%0AUNION%0D%0A%7B%3Fwar+dbpedia-owl%3AwikiPageWikiLink+category-ja%3A%E5%AE%89%E5%9C%9F%E6%A1%83%E5%B1%B1%E6%99%82%E4%BB%A3%E3%81%AE%E6%88%A6%E3%81%84%7D%0D%0A%3Fwar+dbpedia-owl%3Aopponents+%3Fperson+.%0D%0A%7D%0D%0AGROUP+BY+%3Fperson%0D%0AORDER+BY+DESC%28%3Fc%29&format=text%2Fhtml&timeout=0&debug=on
 [28]: http://id.ndl.go.jp/auth/ndla/?query=+select+distinct+*+where%7B%0D%0A++%3Fid+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2Fname%3E+%3Fname.%0D%0A++%3Fid+a+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2FOrganization%3E%3B%0D%0A++%3Chttp%3A%2F%2FRDVocab.info%2FElementsGr2%2FdateOfEstablishment%3E+%3Fdate%3B%0D%0A++%3Chttp%3A%2F%2FRDVocab.info%2FElementsGr2%2FcorporateHistory%3E+%3Fhistory.%0D%0A++filter+%28regex%28str%28%3Fname%29%2C+%22%E5%AD%A6%E4%BC%9A%22%29%29%0D%0A%7D%0D%0Aorder+by+%3Fdate&output=htmltab
 [29]: https://docs.google.com/spreadsheets/d/1zlrplSjBXviaJaEHWBrKqiSYXS1K9ojDKDqOGl5BGOI/edit#gid=0
 [30]: https://github.com/lodac/lodac/wiki/SPARQL%E3%82%B9%E3%83%8B%E3%83%9A%E3%83%83%E3%83%88
 [31]: https://www.mediawiki.org/wiki/Wikibase/Indexing/SPARQL_Query_Examples
 [32]: https://qiita.com/tags/sparql
 [33]: https://gist.github.com/search?q=sparql