#ddl 
DDL: data definition language （数据定义语言），用来定义数据库对象（数据库，表，字段）
## DDL-数据库
```sql
-- 查询所有数据库
show databases;
-- 查询当前数据库
select database();
-- 创建数据库
create database [ if not exists ] 数据库名  [default charset utf8mb4];
-- 使用数据库
use 数据库名;
-- 删除数据库
drop database [ if exists ] 数据库名 ;
```
![[查询所有数据库.png]]
![[查询当前数据库.png]]
![[创建数据库1.png]]![[创建数据库2.png]]

> [!NOTE] 注意
> 1.在同一个数据库服务器中，不能创建两个名称相同的数据库，否则将会报错。
> 2.创建数据库时，可以不指定字符集。 因为在MySQL8版本之后，默认的字符集就是 ==utf8mb4==。
> 3.上述语法中的database可以替换成schema，如：show schemas;
> 4.数据库名以及关键字均可以用大写或者小写，如：DB01 === db01

![[使用数据库.png]]
![[删除数据库.png]]

## DDL-表结构-创建
#表结构-创建
```SQL
create table  表名(
        字段1  字段1类型 [约束]  [comment  字段1注释 ],
        字段2  字段2类型 [约束]  [comment  字段2注释 ],
        ......
        字段n  字段n类型 [约束]  [comment  字段n注释 ] 
) [ comment  表注释 ] ;
```
- 约束：约束是作用于表中字段上的规则，用于限制存储在表中的数据结构
- 目的：保证数据库中的数据正确性、有效性和完整性
### 常见约束
![[数据库常见的5种约束.png]]
- 多个约束用空格分开
- auto_increment 自增关键字
- 主键默认非空且唯一


- 黄色钥匙代表主键
- 蓝色框代表唯一
- 左下角小圆点代表非空
![[datagrip图标解析.png]]

#### 举个例子
```sql
-- 案例设计员工表emp  
-- 基础字段：id 主键 ； create_time 创建时间； update_time 修改时间  
create table emp(  
    id int unsigned primary key auto_increment comment 'ID,主键',  
    username varchar(20) not null unique comment '用户名',  
    password varchar(32) default '123456' comment '密码',  
    name varchar(10) not null comment '姓名',  
    gender tinyint unsigned not null comment '性别： 1.女 2.男',  
    phone char(11) not null unique comment '手机号',  
    job tinyint unsigned comment '职位: 1.班主任 2.讲师 3.学工主管 4.教研主管 5.咨询师',  
    salary int unsigned comment '薪资',  
    entry_date date comment '入职日期',  
    image varchar(255) comment  '头像',  
    create_time datetime comment '创建时间',  
    update_time datetime comment '修改时间'  
)comment '员工表';
```

## DDL-表结构-查询、修改、删除
#DDL-表结构-查询、修改、删除
- 查询数据库表的具体的语法：

```SQL
-- 查询当前数据库的所有表
show tables;

-- 查看指定的表结构
desc 表名 ;   -- 可以查看指定表的字段、字段的类型、是否可以为NULL、是否存在默认值等信息

-- 查询指定表的建表语句
show create table 表名 ;
```

- 修改数据库表结构的具体语法：

添加字段

```SQL
-- 添加字段
alter table 表名 add  字段名  类型(长度)  [comment 注释]  [约束];

-- 比如： 为tb_emp表添加字段qq，字段类型为 varchar(11)
alter table tb_emp add  qq  varchar(11) comment 'QQ号码';
```

修改字段

```SQL
-- 修改字段类型
alter table 表名 modify  字段名  新数据类型(长度);

-- 比如： 修改qq字段的字段类型，将其长度由11修改为13
alter table tb_emp modify qq varchar(13) comment 'QQ号码';
```

```SQL
-- 修改字段名，字段类型
alter table 表名 change  旧字段名  新字段名  类型(长度)  [comment 注释]  [约束];

-- 比如： 修改qq字段名为 qq_num，字段类型varchar(13)
alter table tb_emp change qq qq_num varchar(13) comment 'QQ号码';
```

删除字段

```SQL
-- 删除字段
alter table 表名 drop 字段名;

-- 比如： 删除tb_emp表中的qq_num字段
alter table tb_emp drop qq_num;
```

修改表名

```SQL
-- 修改表名
rename table 表名 to  新表名;

-- 比如: 将当前的emp表的表名修改为tb_emp
rename table emp to tb_emp;
```

删除表结构

```SQL
-- 删除表
drop  table [ if exists ]  表名;

-- 比如：如果tb_emp表存在，则删除tb_emp表
drop table if exists tb_emp;  -- 在删除表时，表中的全部数据也会被删除。
```