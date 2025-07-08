#PathVariable #接收路径参数

@PathVariable注解来声明获取的是路径参数
`/depts/1`，`/depts/2` 这种在url中传递的参数，我们称之为**路径参数**。 那么如何接收这样的路径参数呢 ？

路径参数：通过请求URL直接传递参数，使用{…}来标识该路径参数，需要使用 ==**`@PathVariable`==**获取路径参数。如下所示：

![[接收路径参数.png]]
如果路径参数名与controller方法形参名称一致，`@PathVariable`注解的value属性是可以省略的。

- 在url中是否可以携带多个路径参数呢，如：/depts/1/0？
	- 可以，接收方式如下：
```java
@GetMapping("/depts/#{id}/#{sta}")
public Result getInfo(@PathVariable Integer id, @PathVariable Integer sta){
	//...
}
```