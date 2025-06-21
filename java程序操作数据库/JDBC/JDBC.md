#JDBC
- JDBC:**（Java DataBase Connectivity），就是使用****Java语言操作关系型数据库的一套API****。**
![[JDBC.png]]
**本质：**
- sun公司官方定义的一套操作所有关系型数据库的规范，即接口。
- 各个数据库厂商去实现这套接口，提供数据库驱动jar包。
- 我们可以使用这套接口(JDBC)编程，真正执行的代码是驱动jar包中的实现类。

那有了JDBC之后，我们就可以直接在java代码中来操作数据库了，只需要编写这样一段java代码，就可以来操作数据库中的数据。 示例代码如下：
![[JDBC示例代码.png]]

- 实例与步骤：
	- 依赖
```xml
<dependencies>  
    <!-- MySQL JDBC driver -->  
    <dependency>  
        <groupId>com.mysql</groupId>  
        <artifactId>mysql-connector-j</artifactId>  
        <version>8.0.33</version>  
    </dependency>  
    <dependency>        <groupId>org.junit.jupiter</groupId>  
        <artifactId>junit-jupiter</artifactId>  
        <version>5.9.3</version>  
        <scope>test</scope>  
    </dependency>  
    <dependency>        <groupId>org.projectlombok</groupId>  
        <artifactId>lombok</artifactId>  
        <version>1.18.38</version>  
    </dependency></dependencies>
```

- 代码与步骤（测试类中DML）
```java
import org.junit.jupiter.api.Test;  
  
import java.sql.Connection;  
import java.sql.DriverManager;  
import java.sql.Statement;  
  
public class JdbcTest {  
  
    @Test  
    public void testUpdate() throws Exception {  
        //1.注册驱动  
        Class.forName("com.mysql.cj.jdbc.Driver");  
  
        //2.获取数据库连接  
        String url = "jdbc:mysql://localhost:3306/web01";  
        String username = "root";  
        String password = "1234";  
        Connection connection = DriverManager.getConnection(url, username, password);  
  
        //3.获取SQL语句执行对象  
        Statement statement = connection.createStatement();  
  
        //4.执行SQL  
        int i = statement.executeUpdate("update user set age = 25 where id = 1");//DML  
        System.out.println("SQL执行完毕影响的记录数为：" + i );  
  
        //5.释放资源  
        statement.close();  
        connection.close();  
    }  
  
}
```

- JDBC程序执行DML语句？DQL语句？
	- DML语句：`int rowsAffected = statement.executeUpdate();
	- DQL语句：`ResultSet rs = statement.executeQuery();`
- DQL语句执行完毕结果集ResultSet解析？
	- resultSet.next()：光标往下移动一行
	- resultSet.getXxx()：获取字段数据