#RequestBody #接收json格式请求参数

参数格式：`application/json`
请求参数样例：
```JSON
{
    "name": "教研部"
}
```

- JSON格式的参数，通常会使用一个实体对象进行接收 。
- 规则：JSON数据的==键名==与方法形参==对象的属性名==相同，并需要使用`@RequestBody`注解标识。

前端传递的请求参数格式为json，内容如下：`{"name":"研发部"}`。这里，我们可以通过一个对象来接收，只需要保证对象中有name属性即可。
![[controller中json参数接收.png]]