#Mybatis增删改查
# 删除用户-delete

- 需求：根据ID删除用户信息
- SQL：delete from user where id = 5
- Mapper接口方法：
- 方式一：
```Java
/**
 * 根据id删除
 */
@Delete("delete from user where id = 5")
public void deleteById();
```

这种方式执行删除操作，调用deleteById方法只能删除id为5的用户信息，因为将id直接写死在代码中了，==不可取==。

- 方式二：（==推荐==）
```Java
/**
 * 根据id删除
 */
@Delete("delete from user where id = #{id}")
public void deleteById(Integer id);
```

在Mybatis中，我们可以通过参数占位符号 `#{...}` 来占位，在调用`deleteById`方法时，传递的参数值，最终会替换占位符。

- DML语句执行完毕，是有返回值的，我们可以为Mapper接口方法定义返回值来接收，如下：
    ```Java
    /**
     * 根据id删除
     */
    @Delete("delete from user where id = #{id}")
    public Integer deleteById(Integer id);
    ```

> [!NOTE]
> Integer类型的返回值，表示DML语句执行完毕影响的记录数。

- Mybatis的提供的符号，有两个，一个是 `#{...}`，另一个是 `${...}`，区别如下：

|   |   |   |   |
|---|---|---|---|
|符号|说明|场景|优缺点|
|#{…}|占位符。执行时，会将#{…}替换为?，生成预编译SQL|参数值传递|安全、性能高 （推荐）|
|${…}|拼接符。直接将参数拼接在SQL语句中，存在SQL注入问题|表名、字段名动态设置时使用|不安全、性能低|

**那在企业项目开发中，强烈建议使用 #{...} 。**

# 新增用户 - insert
- 需求：添加一个用户
- SQL：insert into user(username,password,name,age) values ('zhouyu','123456','周瑜',20);
- Mapper接口：
```Java
/**
 * 添加用户
 */
@Insert("insert into user(username,password,name,age) values(#{username},#{password},#{name},#{age})")
public void insert(User user);
```

如果在SQL语句中，我们需要传递多个参数，我们可以把多个参数封装到一个对象中。然后在SQL语句中，我们可以通过`#{对象``属性``名}`的方式，获取到对象中封装的属性值。

单元测试如下：
```java
@Test  
public void testInsert() {  
    User user = new User(null, "caixukun", "8888", "坤", 18);  
    userMapper.insert(user);  
}
```

# 修改用户 - update
- 需求：根据ID更新用户信息
- SQL：update user set username = 'zhouyu', password = '123456', name = '周瑜', age = 20 where id = 1；
- Mapper接口方法：
```Java
/**
 * 根据id更新用户信息
 */
@Update("update user set username = #{username},password = #{password},name = #{name},age = #{age} where id = #{id}")
public void update(User user);
```

单元测试如下：
```java
@Test  
public void testUpdate() {  
    User user = new User(1, "jinx", "888866", "金克斯", 18);  
    userMapper.update(user);  
}
```

# 查询用户 - select
- 需求：根据用户名和密码查询用户信息
- SQL：select * from user where username = 'jinx' and password = '888866';
- Mapper接口：
```Java
/**
 * 根据用户名和密码查询用户信息
 */
@Select("select * from user where username = #{username} and password = #{password}")
public User findByUsernameAndPassword(@Param("username") String username, @Param("password") String password);
```
==@param注解的作用是为接口的方法形参起名字的。（两个以上才需要加）==

（由于用户名唯一的，所以查询返回的结果最多只有一个，可以直接封装到一个对象中）
默认情况下，接口方法当中，在编译的字节码文件时，接口方法形参的名字不会保留，会导致两个传的参数不知道哪个是哪个

单元测试如下：
```Java
@Test
public void testFindByUsernameAndPassword(){
    User user = userMapper.findByUsernameAndPassword("admin666", "123456");
    System.out.println(user);
}
```

**说明：**基于==官方骨架创建的springboot项目==中，接口编译时会保留方法形参名，==@Param注解可以省略== (#{形参名})。
```java
    @Select("select * from user where username = #{username} and password = #{password}")  
//    public User findByUsernameAndPassword(@Param("username") String username, @Param("password") String password);  
    public User findByUsernameAndPassword(String username,String password);
```