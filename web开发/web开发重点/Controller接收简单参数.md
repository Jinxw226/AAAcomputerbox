#RequestParam 

如：/depts?id=1
- **方案一：通过原始的** **`HttpServletRequest`** **对象获取请求参数**

```Java
/**
* 根据ID删除部门 - 简单参数接收: 方式一 (HttpServletRequest)
*/
@DeleteMapping("/depts")
public Result delete(HttpServletRequest request){
    String idStr = request.getParameter("id");
    int id = Integer.parseInt(idStr);
    
    System.out.println("根据ID删除部门: " + id);
    return Result.success();
}
```

这种方案实现较为繁琐，而且还需要进行手动类型转换。**【项目开发很少用】**

- **方案二：通过Spring提供的** **`@RequestParam`** **注解，将请求参数绑定给方法形参**
    

```Java
@DeleteMapping("/depts")
public Result delete(@RequestParam("id") Integer deptId){
    System.out.println("根据ID删除部门: " + deptId);
    return Result.success();
}
```

`@RequestParam` 注解的value属性，需要与前端传递的参数名保持一致 。

```java
@DeleteMapping("/depts")  
public Result delete(@RequestParam(value = "id", required = false) Integer deptId){  
    System.out.println("删除部门id为：" + deptId);  
    return Result.success();  
}
```

> [!NOTE]
> @RequestParam注解required属性默认为true，代表该参数必须传递，如果不传递将报错。 如果参数可选，可以将属性设置为false。

  

- **方案三：如果请求参数名与形参变量名相同，直接定义方法形参即可接收。（省略@RequestParam）**
    

```Java
@DeleteMapping("/depts")
public Result delete(Integer id){
    System.out.println("根据ID删除部门: " + deptId);
    return Result.success();
}
```

对于以上的这三种方案呢，我们==**推荐第三种方案**==。

给参数设置默认值：
`@RequestParam(defaultValue = "1")`