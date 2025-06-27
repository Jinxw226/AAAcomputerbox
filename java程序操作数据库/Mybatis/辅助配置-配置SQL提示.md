#配置SQL提示 #Mybatis
## 配置sql语句提示
默认我们在UserMapper接口上加的 `@Select` 注解中编写SQL语句是没有提示的。
![[配置sql提示1.png]]
![[配置SQL提示2.png]]
![[配置sql提示，语言注入设置.png]]
配置完成之后，发现SQL语句中的关键字有提示了，但还存在不识别表名(列名)的情况：
- 产生原因：Idea和数据库没有建立连接，不识别表信息
- 解决方案：在Idea中配置MySQL数据库连接
![[idea中配置数据库连接.png]]
![[填写数据库信息.png]]

> [!NOTE] 注意
> 该配置的目的，仅仅是为了在编写SQL语句时，有语法提示（写错了会报错），不会影响运行，即使==不配置也是可以的==。
> 在配置的时候指定连接那个数据库，如上图所示连接的就是mybatis数据库（自己的数据库名是什么就指定什么）。

## 配置mybatis日志输出
默认情况下，在Mybatis中，SQL语句执行时，我们并看不到SQL语句的执行日志。 在`application.properties`加入如下配置，即可查看日志：
```Properties
#mybatis的配置
mybatis.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
```

![[配置日志输出.png]]