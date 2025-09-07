#预处理
语法：
```sql
# 定义预处理语句
PREPARE stmt_name FROM preparable_stmt;
# 执行预处理语句
EXECUTE stmt_name [USING @var_name [, @var_name] ...];
# 删除(释放)定义
{DEALLOCATE | DROP} PREPARE stmt_name;
```

PREPARE语句准备好一条SQL语句，并分配给这条SQL语句一个名字供之后调用。准备好的SQL语句通过EXECUTE命令执行，通过DEALLOCATE PREPARE命令释放掉。

语句的名字不区分大小写。准备好的SQL语句名字可以是字符串，也可以是用户指定的包含SQL文本的变量。PREPARE中的SQL文本必须代表一条单独的SQL语句而不能是多条SQL语句。在SQL语句中，? 字符用来作为后面执行查询使用的一个参数。? 不能加上引号，即使打算将它们绑定到字符变量中也不可以 。