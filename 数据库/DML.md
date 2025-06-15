#dml 
DML：data manipulation language（数据操作语言） 用来对数据库中表的数据记录进行增、删、改操作

## DML-insert
```sql
-- 指定字段添加数据
insert into 表名 (字段名1, 字段名2) values (值1, 值2);
-- 全部字段添加数据
insert into 表名 values (值1, 值2, ...);
-- 批量添加数据（指定字段）
insert into 表名 (字段名1, 字段名2) values (值1, 值2), (值1, 值2);
-- 批量添加数据（全部字段）
insert into 表名 values (值1, 值2, ...), (值1, 值2, ...);
```

示例：
```sql
-- DML：数据操作语言  
-- DML：插入数据 - insert-- 1.为emp表的 username， password， name， gender， phone 字段插入值  
insert into emp(username,password,name,gender,phone) values ('songjiang', '12345678','宋江','1','13300001111');  
-- 2.为emp表的所有字段插入值  
insert into emp(id, username, password, name, gender, phone, job, salary, entry_date, image, create_time, update_time)  
        values (null, 'linchong', '12345678', '林冲', 2, '12222222222', 1, 6000, '2020-01-01', '1.jpg',now(),now());  
  
insert into emp  values (null, 'rose', '12345678', '肉丝', 1, '13322222222', 3, 6000, '2020-01-02', '2.jpg',now(),now());  
-- 3.批量为emp表的 username， password， name， gender， phone 字段插入值  
insert into emp(username,password,name,gender,phone)  
    values ('jinx', '123456789','金克斯','1','13300008888'),('v', '123456789','v','1','13300008882');
```

**insert操作的注意事项：**
1. 插入数据时，指定的字段顺序需要与值的顺序是一一对应的。
2. 字符串和日期型数据应该包含在引号中(推荐用单引号)。
3. 插入的数据大小，应该在字段的规定范围内。

## DML-update
```SQL
update 表名 set 字段名1 = 值1 , 字段名2 = 值2 , .... [where 条件] ;
```

示例：
```sql
-- DML: 更新数据 - update-- 1.将emp表的ID为1员工 用户名更新为'zhangsan'，姓名name字段更新为‘张三’  
update emp set username = 'zhangsan', name = '张三' where id = 1;  
-- 2.将emp表的所有员工的入职日期更新为 '2004-01-01'
update emp set entry_date = '2004-01-01';
```

**注意事项:**
1. 修改语句的条件可以有，也可以没有，如果没有条件，则会修改整张表的所有数据。
2. 在修改数据时，一般需要同时修改公共字段update_time，将其修改为当前操作时间。

## DML-delete
```SQL
delete from 表名  [where  条件] ;
```

示例：
```sql
-- DML: 删除数据 -delete-- 1.删除 emp 表中 ID为1的员工  
delete from emp where id = 1;  
-- 2.删除 emp 表中的所有员工  
delete from emp ;
```

**注意事项:**
- DELETE 语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据。
- DELETE 语句不能删除某一个字段的值(可以使用UPDATE，将该字段值置为NULL即可)。
- 当进行删除全部数据操作时，会提示询问是否确认删除所有数据，直接点击Execute即可。