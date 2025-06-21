#JDBC-查询数据 #JDBC

> [!代码实现ai提示词]
> 你是一名java开发工程师，帮我基于JDBC程序来操作数据库，执行如下SQL语句：
> select * from user where username = 'daqiao' and password = '123456'
> 并讲查询的每一行记录，都封装到实体类User中，然后将User对象的数据输出到控制台中。
> User实体类如下：


```java
@Data  
@AllArgsConstructor  
//全参构造  
@NoArgsConstructor  
//无参构造  
public class User {  
    private Integer id;  
    private String username;  
    private String password;  
    private String name;  
    private Integer age;  
}
```

ResultSet（结果集对象）：封装了DQL查询语句查询的结果。

- next()：将光标从当前位置向前移动一行，并判断当前行是否为有效行，返回值为boolean。
    - true：有效行，当前行有数据
    - false：无效行，当前行没有数据
- getXxx(…)：获取数据，可以根据列的编号获取，也可以根据列名获取（推荐）。

实例：
```java
@Test  
public void testSelect () throws Exception{  
    String URL = "jdbc:mysql://localhost:3306/web01";  
    String USERNAME = "root";  
    String PASSWORD = "1234";  
  
    Connection conn = null;  
    PreparedStatement  pstmt = null;  
    //1.注册驱动  
    Class.forName("com.mysql.cj.jdbc.Driver");  
    //2.获取数据库连接  
    conn = DriverManager.getConnection(URL, USERNAME, PASSWORD);  
    // 创建预编译的PreparedStatement对象  
    pstmt = conn.prepareStatement("select * from user where username = ? and password = ?");  
    // 设置参数  
    pstmt.setString(1, "daqiao"); // 第一个问号对应的参数  
    pstmt.setString(2, "123456"); // 第二个问号对应的参数  
    ResultSet rs = pstmt.executeQuery();  
    // 处理结果集  
    while (rs.next()) {  
        int id = rs.getInt("id");  
        String uName = rs.getString("username");  
        String pwd = rs.getString("password");  
        String name = rs.getString("name");  
        int age = rs.getInt("age");  
        System.out.println("ID: " + id + ", Username: " + uName + ", Password: " + pwd + ", Name: " + name + ", Age: " + age);  
    }  
    // 关闭资源  
    rs.close();  
    pstmt.close();  
    conn.close();  
}
```

- JDBC程序执行DML语句：int rowsUpdated = pstmt.executeUpdate(); //返回值是影响的记录数
- JDBC程序执行DQL语句：ResultSet resultSet = pstmt.executeQuery(); //返回值是查询结果集