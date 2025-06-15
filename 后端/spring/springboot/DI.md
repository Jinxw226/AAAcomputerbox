#DI #DI详解
- 基于@Autowired进行依赖注入的常见方式有如下三种：
- 属性注入
	- 优点：代码简洁，方便快速开发   
	- 缺点:隐藏了类之间的依赖关系，可能会破坏类的封装性
![[DI.属性注入.png]]
- 构造函数注入
	- 优点：能清晰的看到类的依赖关系，提高代码的安全性
	- 缺点：代码繁琐，如果构造参数过多，可能会导致构造函数臃肿
	- 注意：如果只有一个构造函数，@Autowired注解可以省略
![[DI.构造函数注入.png]]
- setter注入
	- 优点：保持了类的封装性，依赖关系更清晰
	- 缺点：需要额外编写setter方法，增加了代码量
![[DI.setter注入.png]]

```java
	//方法一：属性注入  
    @Autowired//将service注入到controller  
    private UserService userService;  
    //方法二：构造器注入  
    private final UserService userService;  
    @Autowired --> 如果当前类中只存在一个构造函数，则@Autowired可以省略  
    public UserController(UserService userService) {  
        this.userService = userService;  
    }  
    //方式三：setter注入  
    private UserService userService;  
    @Autowired  
    public void setUserService(UserService userService) {  
        this.userService = userService;  
    }
```

![[多个bean引发的错误处理.png]]@Resource与@Autowired区别
- @Autowired是Spring框架提供的注解，而@Resource是JavaEE规范提供的
- @Autowired默认是按照类型注入，而@Resource默认是按照名称注入的