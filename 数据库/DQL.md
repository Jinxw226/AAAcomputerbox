#dql 
DQL：Data query language（数据查询语言），用来查询数据库表中的记录
关键字：==select==
语法结构：
```SQL
SELECT
        字段列表
FROM
        表名列表
WHERE
        条件列表
GROUP  BY
        分组字段列表
HAVING
        分组后条件列表
ORDER BY
        排序字段列表
LIMIT
        分页参数
```
- 五种查询：
	- 基本查询（不带任何条件）
	- 条件查询（where）
	- 分组查询（group by）
	- 排序查询（order by）
	- 分页查询（limit）

## 基本查询
```SQL
-- 查询多个字段
select 字段1, 字段2, 字段3 from  表名;
-- 查询所有字段（通配符）
select *  from  表名;
-- 设置别名
select 字段1 [ as 别名1 ] , 字段2 [ as 别名2 ]  from  表名;
-- 去除重复记录
select distinct 字段列表 from  表名;
```


