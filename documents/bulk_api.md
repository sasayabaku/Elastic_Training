# Bulk API

大量のdocumentを処理する場合に利用

```bash
curl -H "Content-Type: application/x-ndjson" -XPOST http://localhost:9200/aozora/_bulk?pretty --data-binary @data/aozora.json
```

# 条件指定のデータ取得
## ORで複数のデータを取得

```bash
curl -H "Content-Type: application/json" http://localhost:9200/aozora/_search -d \
'{
    "query": {
        "match": {
            "id": "002 003"
        }
    }
}'
```
「吾輩は猫である」と「学問のすすめ」の両方がヒットする。

## ANDでのデータ取得
ANDの場合は、`要素` 内に、`operator:"and"` を記述。

```json
・・・
"match": {
    "id": {
        "query": "002 003",
        "operator": "and"
    }
}
・・・
```
idは、一意なのでヒット数0で返ってくる。

## minumum_should_match | OR と ANDの間
ORでは緩すぎ、ANDでは厳しすぎる場合に、query内のN個の要素が含まれればOKというクエリ。

※ 重複した語もカウント

冒頭一文のデータである。 `beggining` を検索してみる。

```bash
curl -H "Content-Type: application/json" http://localhost:9200/aozora/_search -d \
'{
    "query": {
        "match": {
            "beggining": {
                "query": "ある 名前 吾輩 天",
                "minimum_should_match": 2
            }
        }
    }
}'
```

この場合、  
* 「ある」「吾輩」「名前」を含む 吾輩は猫である
* 「ある」「天」を含む 学問のすすめ

の両者がヒットする。