```bash
GET /old_index/_search?scroll=1m
{
    "query": { "match_all": {}},
    "sort" : ["_doc"], [](https://www.elastic.co/guide/cn/elasticsearch/guide/current/scroll.html#CO32-2)
    "size":  1000
}
```
- 保持游标查询窗口一分钟。
- 关键字`_doc`是最有效的排序顺序。

这个查询的返回结果包括一个字段`_scroll_id`，它是一个base64编码的长字符串。现在我们能传递字段`_scroll_id`到`_search/scroll`查询接口获取下一批结果：
```bash
GET /_search/scroll
{
    "scroll": "1m",
    "scroll_id" : "cXVlcnlUaGVuRmV0Y2g7NTsxMDk5NDpkUmpiR2FjOFNhNnlCM1ZDMWpWYnRROzEwOTk1OmRSamJHYWM4U2E2eUIzVkMxalZidFE7MTA5OTM6ZFJqYkdhYzhTYTZ5QjNWQzFqVmJ0UTsxMTE5MDpBVUtwN2lxc1FLZV8yRGVjWlI2QUVBOzEwOTk2OmRSamJHYWM4U2E2eUIzVkMxalZidFE7MDs="
}
```
- 注意再次设置游标查询过期时间为一分钟。

[[基础入门/执行分布式检索/readme|返回]]