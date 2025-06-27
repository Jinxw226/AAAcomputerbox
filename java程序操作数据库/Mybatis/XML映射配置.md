#XML映射配置
- 在Mybatis中，既可以通过注解配置SQL语句，也可以通过XML文件配置SQL语句
- 默认规则：
	1. XML映射文件的名称与Mapper接口名称一致，并且将XML映射文件和Mapper接口放置在相同包下（同包同名）
	2. XML映射文件的namespace属性为Mapper接口全限定名一致
	3. XML映射文件中sql语句的id与Mapper接口中的方法名一致，并保持返回类型一致。
![[xml映射配置.png]]`<select>`标签：就是用于编写select查询语句的。
resultType属性，指的是查询返回的单条记录所封装的类型。

# xml配置文件实现
**第1步：创建XML映射文件**
![[新建包-xml配置.png]]
![[创建包.png]]
**第2步：编写XML映射文件**
xml映射文件中的dtd约束，直接从mybatis官网复制即可; 或者直接AI生成。
```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="">
 
</mapper>
```

实例：
```XML
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE mapper  
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">  
<mapper namespace="com.itjf.mapper.UserMapper">  
    <select id="findAll" resultType="com.itjf.pojo.User">  
        select id, username, password, name, age from user  
    </select>  
</mapper>
```

**注意：一个接口方法对应的SQL语句，要么使用注解配置，要么使用XML配置，切不可同时配置。**
## XML映射文件

Q：那么在Mybatis的开发中，到底是用注解开发还是使用XML开发呢？
A：使用Mybatis注解，主要是来完成一些假肚腩的增删改查功能。如果需要实现复杂的SQL功能，建议使用XML配置映射语句。

### XML映射文件-辅助配置
如果XML映射文件的名称与Mapper接口不同包，则可以通过在properties文件中添加这个一行话来继续让文件实行
```properties
#指定XML映射配置文件的位置
mybatis.mapper-locations=classpath:mapper/*.xml
```
![[XML文件同名不同包.png]]