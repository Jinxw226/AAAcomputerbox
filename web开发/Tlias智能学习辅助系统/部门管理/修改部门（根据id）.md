# 查询回显
**1). Controller层**
在 `DeptController` 中增加 `getById`方法，具体代码如下：

```Java
/**
 * 根据ID查询 - GET http://localhost:8080/depts/1
 */
@GetMapping("/depts/{id}")
public Result getById(@PathVariable Integer id){
    System.out.println("根据ID查询, id=" + id);
    Dept dept = deptService.getById(id);
    return Result.success(dept);
}
```

**2). Service层**
在 `DeptService` 中增加 `getById`方法，具体代码如下：
```Java
/**
 * 根据id查询部门
 */
Dept getById(Integer id);
```

在 `DeptServiceImpl` 中增加 `getById`方法，具体代码如下：

```Java
public Dept getById(Integer id) {
    return deptMapper.getById(id);
}
```

**3). Mapper层**
在 `DeptMapper` 中增加 `getById` 方法，具体代码如下：

```Java
/**
* 根据ID查询部门数据
*/
@Select("select id, name, create_time, update_time from dept where id = #{id}")
Dept getById(Integer id);
```

# 需求分析
**1). Controller层**
在 `DeptController` 中增加 `update` 方法，具体代码如下：

```Java
/**
 * 修改部门 - PUT http://localhost:8080/depts  请求参数：{"id":1,"name":"研发部"}
 */
@PutMapping("/depts")
public Result update(@RequestBody Dept dept){
    System.out.println("修改部门, dept=" + dept);
    deptService.update(dept);
    return Result.success();
}
```

**2). Service层**
在 `DeptService` 中增加 `update` 方法。

```Java
/**
 * 修改部门
 */
void update(Dept dept);
```

在 `DeptServiceImpl` 中增加 `update` 方法。 由于是修改操作，每一次修改数据，都需要更新updateTime。所以，具体代码如下：

```Java
public void update(Dept dept) {
    //补全基础属性
    dept.setUpdateTime(LocalDateTime.now());
    //保存部门
    deptMapper.update(dept);
}
```

**3). Mapper层**
在 `DeptMapper` 中增加 `update` 方法，具体代码如下：

```Java
/**
 * 更新部门
 */
@Update("update dept set name = #{name},update_time = #{updateTime} where id = #{id}")
void update(Dept dept);
```