## 索引概述

我们常常会看到一些乱七八糟的索引，所以我们用索引的真正目的是什么呢？

终极目的：借助索引快速搜索，有效减少了扫描的行数

精髓：不止要有索引，索引的过滤性还要好，区分度要足够高，这才是好的设计

## 核心区别
- 没有索引全表扫描，放到内存中排序.
- 有索引按照索引先排好序，避免全表扫描.

## 索引种类
- _id索引  {_id: 1}
- 单键索引 {a: 1}
- 复合索引 {a: 1, b: 1}
- 多值索引 { a.b: 1 }
- 地理位置索引 还不是太会用... db.map.ensureIndex({"gps" : "2d"})
- 全文索引 db.<collection_name>.createIndex({<key>: "text"}) / db.<collection_name>.find( { $text: { $search: "green" } } );
- ttl索引 db.user_session.createIndex({"updated":1},{expireAfterSeconds:60*60*24});
- 部分索引
- 稀疏索引
- 哈希索引 db.collection.createIndex( { _id: "hashed" }) 哈希索引指按照某个字段的hash值来建立索引，目前主要用于MongoDB Sharded Cluster的Hash分片，hash索引只能满足字段完全匹配的查询，不能满足范围查询


## 参考

https://zhuanlan.zhihu.com/p/77971681