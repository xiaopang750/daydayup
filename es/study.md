## match

```
{
  "query": {
    "match": {
      "xhs_school_target.button_name": {
        "query": "细分来源",
        "type": "phrase"
      }
    }
  }
}
```

- term是将传入的文本原封不动地（不分词）拿去查询。
- match会对输入进行分词处理后再去查询，部分命中的结果也会按照评分由高到低显示出来。
- match_phrase是按短语查询，只有存在这个短语的文档才会被显示出来。


## 查询url params

- 例如 /api/cs/v2/seller/12312312312312/messages 可以这样查询 /api/cs/v2/seller AND /messages
- or
```
{
  "query": {
    "regexp": {
      "request.keyword": "/api/.*/messages",
    }
  }
}
```
