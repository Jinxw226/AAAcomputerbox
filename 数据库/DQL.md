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
## 条件查询
![[条件运算符.png]]
```SQL
select  字段列表  from   表名   where   条件列表 ; -- 条件列表：意味着可以有多个条件
```
注意：
- between之后跟的是最小的值，and后面跟的是最大的值，顺序不可以随便调换
- in是满足括号内的任一个条件即可被筛选出
- is null，is not null
-  '_':单个字符  %：任意个字符

实例：
```sql
# 条件查询  
# 查询没有分配职位的员工信息  
select * from emp where job is null;  
  
# 查询密码不等于'123456'的员工信息  
select * from emp where password != '123456';  
  
# 查询 入职日期在 '2000-01-01'(包含) 到 '2010-01-01'(包含) 之间的员工信息  
select * from emp where entry_date between '2000-01-01' and '2010-01-01';  
select * from emp where entry_date between '2000-01-01' and '2010-01-01' and gender = 2;  
select * from emp where job = 2 or job = 3 or job = 4;  
select * from emp where job in (2,3,4);  
  
# 查询姓名为两个字的员工信息（_:单个字符  %：任意个字符）  
select * from emp where name like '__';  
  
# 查询 姓'阮' 的员工信息  
select * from emp where name like '阮%';  
  
# 查询姓名中包含 '二' 的员工信息  
select * from emp where  name like '%二%';
```

## 分组查询
- 聚合函数：将一列数据作为一个整体进行纵向计算
![[分组查询函数.png]]注意：
- null值不参与所有的聚合函数的统计
- 统计量可以使用：count（*）*，count（常量），count（字段），推荐使用count（✳）
实例：
```sql
#分组查询(聚合函数)  
# 统计企业员工数量 - count-- count(字段)  
select count(id) from  emp;  
-- count(*) 统计总数据量  ：优先推荐使用！  
select count(*) from  emp;  
-- count(常量) 检测存在就一个1  ：和count*差不多  
select count(1) from  emp;  
  
#统计该企业员工的平均薪资 - avg
select avg(salary) from emp;  
  
#统计该企业员工的最高薪资 - max
select max(salary) from emp;  
  
#统计该企业员工的最低薪资 - min
select min(salary) from emp;  
  
# 统计每月发工资总和（薪资之和） - sum
select sum(salary) from emp;
```

分组
```SQL
select  字段列表  from  表名  [where 条件]  group by 分组字段名  [having 分组后过滤条件];
```
- where和having的区别：
	- 执行时机不同：where是分组之前进行过滤，不满足where条件，不参与分组；而having是分组之后对结果进行过滤
	- 判断条件不同：where不能对集合函数进行判断，而having可以
注意：
- 分组之后， select后的字段列表不能随意书写，能写的一般是 分组字段 + 聚合函数
- 执行顺序： where > 聚合函数  > having
实例：
```sql
#分组  
-- 根据性别分组，统计女性和男性员工的数量  
select gender, count(*) from emp group by gender;  

-- 先查询入职时间在 '2015-01-01'(包含) 以前的员工，并对结果根据职位分组，获取员工数量大于等于2的职位  
select job, count(*) from emp where entry_date <= '2015-01-01' group by job having count(*) >= 2;
```

## 排序查询
```SQL
select  字段列表  
from   表名   
[where  条件列表] 
[group by  分组字段 ] 
order  by  字段1  排序方式1 , 字段2  排序方式2 … ;
```
- 排序方式：
    - ASC ：升序（默认值，可以不写）
    - DESC：降序
注意：
- 如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序

实例：
```sql
#排序查询  
# 根据入职时间，对员工进行升序排序 - ascselect * from emp order by entry_date asc;  
select * from emp order by entry_date ;  

# 根据入职时间，对员工进行降序排序 - descselect * from emp order by entry_date desc;  

# 根据入职时间 对公司员工进行 升序排序， 入职时间相同，再按照 更新时间 进行降序排序  
select * from emp order by entry_date , update_time desc;
```

## 分页查询
```SQL
select  字段列表  from  表名  limit  起始索引, 查询记录数 ;
```
注意：
- 起始索引从0开始
- 分页查询是数据库的方言，不同数据库有不同的实现，mysql中是LIMIT
- 如果起始索引为0，起始索引可以省略，直接简写为 limit 10
- 起始索引 = （页码 - 1）* 每页展示记录数
实例：
```sql
# 分页查询  
-- 从起始索引0开始查询员工数据，每一页展示5条数据  
select * from emp limit 0, 5;  
select * from emp limit 5;  
-- 查询第1页的员工数据，每页展示5条记录  
select * from emp limit 1, 5;  
-- 查询第2页的员工数据，每页展示5条记录  
select * from emp limit 5, 5;  
-- 查询第3页的员工数据，每页展示5条记录  
select * from emp limit 10, 5;  

-- 页码  
-- 起始索引 = （页码 - 1）* 每页展示记录数
```