# Bulk API

大量のdocumentを処理する場合に利用

```bash
$ curl -H "Content-Type: application/x-ndjson" -XPOST http://localhost:9200/aozora/_bulk?pretty --data-binary @data/aozora.json
```

## ORで複数のデータを取得

```bash
$ curl -H "Content-Type: application/json" http://localhost:9200/aozora/_search -d \
'{
    "query": {
        "match": {
            "id": "002 003"
        }
    }
}'
```
「吾輩は猫である」と「学問のすすめ」の両方がヒットする。