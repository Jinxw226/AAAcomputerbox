#RequestMapping 
@RequestMapping可以加在：
- 类上
- 方法上
- 完整=类+方法上

我们可以把公共的路径/depts抽取到类上，那在各个方法上，就可以省略了这个 `/depts` 路径。
![[提取公共路径至类上.png]]

> [!NOTE]
> 一个完整的请求路径，应该是类上的 @RequestMapping 的value属性 + 方法上的 @RequestMapping的value属性。