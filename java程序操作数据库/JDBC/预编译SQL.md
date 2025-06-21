#预编译SQl #PreparedStatement 
# 预编译SQL
- 优势一：可以防止SQL注入，更安全
- 优势二：性能更高
![[预编译优势性能更高.png]]

- 静态SQL（参数硬编码）
```Java
conn.prepareStatement("SELECT * FROM user WHERE username = 'daqiao' AND password = '123456'");
ResultSet resultSet = pstmt.executeQuery();
```
这种呢，就是参数值，直接拼接在SQL语句中，参数值是写死的。

- 预编译SQL（参数动态传递）
```Java
conn.prepareStatement("SELECT * FROM user WHERE username = ? AND password = ?");
pstmt.setString(1, "daqiao");
pstmt.setString(2, "123456");
ResultSet resultSet = pstmt.executeQuery();
```

这种呢，并未将参数值在SQL语句中写死，而是使用 ？ 进行占位，然后再指定每一个占位符对应的值是多少，而最终在执行SQL语句的时候，程序会将SQL语句（SELECT * FROM user WHERE username = ? AND password = ?），以及参数值（"daqiao", "123456"）都发送给数据库，然后在执行的时候，会使用参数值，将？占位符替换掉。

预编译SQL主要功能：
- 防止SQL注入
- 性能更高

## SQl注入
- SQL注入：通过控制输入来修改事先定义好的SQL语句，以达到执行代码对服务器进行攻击的方法。
注入演示：
1). 打开课程资料中的文件夹 `资料/02. SQL注入演示`，运行其中的jar包 `sql_Injection_demo-0.0.1-SNAPSHOT.jar`，进入该目录后，执行命令：
```Java
java -jar sql_Injection_demo-0.0.1-SNAPSHOT.jar
```
![[sql注入（不是预编译版本）.png]]2). 打开浏览器访问 http://localhost:9090/ ，必须登录后才能访问到系统。我们先测试正常的用户名和密码
`' or '1' = '1`这个代码改变了sql语句的意思，即使用户名密码输入错误，也是可以查询返回结果的，而只要查询到了数据，就说明用户名和密码是正确的。

## SQL注入解决
而通过预编译SQL（select * from user where username = ? and password = ?），就可以直接解决上述SQL注入的问题。 接下来，我们再来演示一下，通过预编译SQL是否能够解决SQL注入问题。
1). 打开课程资料中的文件夹 `资料/02. SQL注入演示`，运行其中的jar包 `sql_prepared_demo-0.0.1-SNAPSHOT.jar`，进入该目录后，执行命令：
```Java
java -jar sql_prepared_demo-0.0.1-SNAPSHOT.jar
```
2). 那接下来，我们就要演示一下是否可以基于上述的密码 `' or '1' = '1`，来完成SQL注入 。
而在预编译SQL语句中，当我们执行的时候，会把整个`' or '1'='1`作为一个完整的参数，赋值给第2个问号（`' or '1'='1`进行了转义，只当做字符串使用）

那么此时再查询时，就查询不到对应的数据了，登录失败。

> [!NOTE] 注意
> 在以后的项目开发中，我们使用的基本全部都是预编译SQL语句。
