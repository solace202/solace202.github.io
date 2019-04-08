## MySQL优化

###### 如果明确知道查询结果只有一条记录，建议使用 limit 1 来提高效率，可以让数据库停止游标的移动

`select name from user where id=6105281991******** limit 1`

#### 索引（index）：

对于记录较多的表在使用时可以提高检索速度，分为单列索引和组合索引。

普通索引：create index index_name on user(id, ..., ...);

UNIQUE索引：create unique index index_name on user(id, ..., ...);

主键索引：create table user( [...], PRIMARY KEY (id, ..., ...) ); 
索引选择原则：

* 较频繁的作为查询条件的字段
* 唯一性太差的字段不适合创建索引
* 更新太频繁的字段不适合作为索引






































