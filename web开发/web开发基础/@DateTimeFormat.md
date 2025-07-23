#DateTimeFormat
@DateTimeFormat(pattern = "yyyy-MM-dd")

```java
@GetMapping  
public Result page(@RequestParam(defaultValue = "1") Integer page,  
                   @RequestParam(defaultValue = "10") Integer pageSize,  
                   String name, Integer gender,  
                   @DateTimeFormat(pattern = "yyyy-MM-dd") LocalDate begin,  
                   @DateTimeFormat(pattern = "yyyy-MM-dd") LocalDate end){  
    log.info("分页查询，参数：{},{},{},{},{},{}", page, pageSize,name,gender,begin,end);  
    PageResult<Emp>  pageResult = empService.page(page, pageSize, name, gender, begin, end);  
    return Result.success(pageResult);  
}
```