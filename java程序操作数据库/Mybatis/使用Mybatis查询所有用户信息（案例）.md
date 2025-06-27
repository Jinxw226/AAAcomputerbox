#mybatis查询案例 
- 准备工作
	- 创建springboot工程，引入mybatis相关依赖
![[mybatis查询所有用户信息-创建springboot.png]]
![[mybatis依赖.png]]
- 准备数据库表User，实体类User
- 配置mybatis，编写mybatis的持久层接口，定义sql（注解、xml）（在application.properties中的数据库连接信息）
![[配置文件字符集设定.png]]
```Properties
#数据库访问的url地址
spring.datasource.url=jdbc:mysql://localhost:3306/web
#数据库驱动类类名
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
#访问数据库-用户名
spring.datasource.username=root
#访问数据库-密码
spring.datasource.password=root@1234
```
![[mapper接口定义.png]]
```Java
import com.itheima.pojo.User;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Select;
import java.util.List;

@Mapper
public interface UserMapper {
    /**
     * 查询全部
     */
    @Select("select * from user")
    public List<User> findAll();
}
```
- 编写测试类
```java
@SpringBootTest  //springboot单元测试注解 - 当前测试类中的测试方法运行时，会启动整个springboot项目 - IOC容器  
class SpringbootMybatisQuickstartApplicationTests {  
  
    @Autowired  
    private UserMapper  userMapper;  
  
    @Test  
    public void testFindAll() {  
        List<User> userlist = userMapper.findAll();  
        userlist.forEach(System.out::println);  
    }  
}
```

> [!NOTE] 注意
> 测试类所在包，需要与引导类所在包相同。
